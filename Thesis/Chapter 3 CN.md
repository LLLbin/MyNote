### Overview of Proposed Model
本文提出的超分辨率模型基于VQGAN架构，并结合了ConvNeXt特征提取模块，整个的网络架构如图figure3-1所示，主要包括以下五个部分：编码器（Encoder）、ConvNeXt特征提取器、码本（Codebook）、解码器（Decoder）和判别器（Discriminator）。我们方法的整体训练由两个阶段组成。在第一阶段，我们主要训练VQGAN的骨架网络，其中包括Encoder，Codebook，Decoder，用来提取HR图像中的高分辨率先验信息来进行第二阶段的超分辨任务。在第二阶段，我们结合了第一阶段的固定码本和固定图像解码器训练Encoder，ConvNeXt特征提取器以及Discriminator，用以解决图像盲超分辨率的任务。
#### Encoder

编码器的主要任务是将输入的低分辨率图像进行特征提取和压缩。我们采用了VQGAN中的编码器结构，通过n个下采样器将低分辨率图像转换为紧凑的特征表示 $\hat{x}$，其中每个下采样器都将图像的Height和Weight都减少一半。如果给到输入图像 $x ∈ \mathbb{R}^{H \times W \times 3}$，那么经过VQ-Encoder处理后就输出$\hat{x} \in \mathbb{R}^{\frac{H}{2^n} \times \frac{W}{2^n} \times n_{\hat{x}}}$。这种表示不仅保留了图像中的重要信息，而且减少了特征的空间维度，为后续的特征处理和量化打下基础。
#### ConvNeXt

为了进一步增强特征提取能力，我们在编码器之后引入了基于卷积神经网络的ConvNeXt模块，其模型结构如图figure3-2所示。ConvNeXt模块主要由3 parts来组成。
- Stem layer，使用 `4x4` 的卷积核进行下采样大幅度缩减输入图像的尺寸，减少运算复杂度，提升后续模块运行的速度和效率。此外还接入 LayerNorm 进行归一化，这有助于网络训练的稳定性和模型性能的提升。
- 四个阶段的特征提取（Stages），每个阶段的开始都使用了下采样层，进一步减小特征图的尺寸，每个下采样层通常使用 `2x2` 的卷积核和步长为2。接着是一系列的卷积块（Blocks），其中每个卷积块（Block）都使用了深度卷积（DwConv）技术来提取空间特征，接着使用排列和标准化提升训练过程中的数值稳定性，最后使用两个线性层进行特征转换并使用GELU 激活函数连接他们。在每个卷积块的末尾，会将处理过的特征与块输入直接相加，形成跳跃连接，以便引入残差学习。此外，添加了DropPath（一种随机深度技术），以增强模型的泛化能力和鲁棒性。
- Upsampler Layers，使用了 PixelShuffle 技术进行上采样，以便满足 codebook 的输入尺寸要求。
ConvNeXt模块利用卷积操作在保留空间信息的同时提取更加丰富的图像特征，从而提高了模型对低分辨率图像特征的捕捉能力，使得生成的高分辨率图像更为清晰和细腻。
#### Codebook

输入的HR图像 $y \in \mathbb{R}^{H \times W \times 3}$，经过Encoder的处理后，输出的特征表示 $\hat{z} = E(y) \in \mathbb{R}^{h \times w \times n_\hat{z}}$ 会通过码本进行量化。码本包含多个离散的特征向量，
用于表示输入图像的不同部分。在量化的过程中，每个输入的 $\hat{z}_{i} \in \mathbb{R}^{n_\hat{z}}$ 都会被替换成codebook $Z \in \mathbb{R}^{K \times n_{z}}$ 中最接近的code来构造量化嵌入 $z_{qk} \in \mathbb{R}^{n_\hat{z}}$ 。
$$z_\mathbf{q}=\mathbf{q}(\hat{z})=\left(\underset{z_k\in\mathcal{Z}}{\operatorname*{\arg\min}}\|\hat{z}_{i}-z_k\|\right)\in\mathbb{R}^{h\times w\times n_z}$$
其中，$K$ 是codes在codebook中的总数量，$i \in \{1,2,\dots,h\times w$ 。在这之后，y 由 z 通过解码器 G 重建： 
$$\hat{y}=G(z_{q})\approx y$$
通过量化过程，模型能够有效地压缩和表示图像的特征，并增强图像生成的多样性和准确性。
#### Decoder

解码器的任务是将量化后的特征表示 zqz_qzq​ 转换回高分辨率图像。我们使用了VQGAN中的解码器结构，通过一系列反卷积层和非线性激活函数逐步恢复图像的细节和纹理。解码器不仅要生成高质量的图像，还要确保生成的图像在视觉上逼真和自然。
#### Discriminator

为了提高生成图像的质量，我们引入了生成对抗网络（GAN）中的判别器模块。判别器用于区分生成的高分辨率图像和真实的高分辨率图像。通过对抗训练，生成器（即编码器、ConvNeXt和解码器的组合）不断提升自身能力，以生成能够骗过判别器的高质量图像。这种对抗机制有效地提高了模型生成图像的逼真度和细节还原能力。