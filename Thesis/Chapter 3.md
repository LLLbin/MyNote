### Overview of Proposed Model
本文提出的超分辨率模型基于VQGAN架构，并结合了ConvNeXt特征提取模块。整个网络架构如图3-1所示，主要包括编码器（Encoder）、ConvNeXt特征提取器、码本（Codebook）、解码器（Decoder）和判别器（Discriminator）。首先，低分辨率图像（LR图像）$x$ 经过编码器进行压缩与编码，得到的结果 $\hat{x}$ 进入ConvNeXt模块进行深度特征提取。随后，提取到的连续特征 $\hat{z}$ 在码本中被量化为离散形式 $z_{q}$，再由解码器将量化后的特征表示 $z_{q}$ 重建为高分辨率图像。最后，通过判别器对超分辨率图像和高分辨率图像进行判别，对抗性训练提升了生成图像的逼真度和细节还原能力。
#### Encoder

编码器的主要任务是将输入的低分辨率图像进行特征提取和压缩。编码器结构由多个下采样器组成，可以将低分辨率图像转换为紧凑的特征表示 $\hat{x}$。每个下采样器都会将图像的高度和宽度减少一半。具体来说，给定输入图像 $x \in \mathbb{R}^{H \times W \times 3}$，经过VQ-编码器处理后，输出特征表示 $\hat{x} \in \mathbb{R}^{\frac{H}{2^n} \times \frac{W}{2^n} \times n_{\hat{x}}}$。这种特征表示不仅保留了图像中的重要信息，还减少了特征的空间维度，为后续的特征处理和量化奠定了基础。
#### ConvNeXt

为了进一步增强特征提取能力，我们在编码器之后引入了基于卷积神经网络的ConvNeXt模块，其模型结构如图3-2所示。ConvNeXt模块主要由以下三个部分组成：

- **Stem层**：使用 `4x4` 的卷积核进行下采样，大幅度缩减输入图像的尺寸，从而减少计算复杂度，提高后续模块的运行速度和效率。此外，还引入了LayerNorm进行归一化，有助于提高网络训练的稳定性和模型性能。
- **四个阶段的特征提取（Stages）**：每个阶段开始时都会使用下采样层，进一步减小特征图的尺寸。每个下采样层通常使用 `2x2` 的卷积核，步长为2。随后是一系列的卷积块（Blocks），其中每个卷积块使用深度卷积（DwConv）技术提取空间特征，接着进行排列和标准化以提升训练过程中的数值稳定性，最后通过两个线性层进行特征转换，并使用GELU激活函数连接它们。在每个卷积块的末尾，会将处理过的特征与块输入直接相加，形成跳跃连接，以引入残差学习。此外，添加了DropPath（一种随机深度技术），以增强模型的泛化能力和鲁棒性。
- **上采样层（Upsampler Layers）**：使用PixelShuffle技术进行上采样，以满足码本（codebook）的输入尺寸要求。

ConvNeXt模块通过卷积操作在保留空间信息的同时提取更加丰富的图像特征，从而提高了模型对低分辨率图像特征的捕捉能力，使生成的高分辨率图像更加清晰和细腻。
#### Codebook

在VQGAN中，码本（Codebook）是一个关键组件，其主要作用是将连续的特征向量量化为离散的表示，从而减少表示的复杂性并提高生成图像的质量和连贯性。通过学习使编码后的特征向量接近代码向量（Code Vectors），从而将连续的表示映射到一个离散的集合中，大幅降低特征表示的复杂性。此外，VQGAN中使用了向量量化技术（Vector Quantization）和替代梯度（Straight-Through Estimator）更新码本，确保模型各部分能够有效训练。

具体来说，输入的高分辨率图像 $y \in \mathbb{R}^{H \times W \times 3}$ 经过编码器处理后，输出的特征表示 $\hat{z} = E(y) \in \mathbb{R}^{h \times w \times n_\hat{z}}$ 会通过码本进行量化。码本包含多个离散的特征向量，用于表示输入图像的不同部分。在量化过程中，每个输入的 $\hat{z}_{i} \in \mathbb{R}^{n_\hat{z}}$ 都会被替换成码本 $Z \in \mathbb{R}^{K \times n_{z}}$ 中最接近的代码向量来构造量化嵌入 $z_{qk} \in \mathbb{R}^{n_\hat{z}}$ 。
$$z_\mathbf{q}=\mathbf{q}(\hat{z})=\left(\underset{z_k\in\mathcal{Z}}{\operatorname*{\arg\min}}\|\hat{z}_{i}-z_k\|\right)\in\mathbb{R}^{h\times w\times n_z}$$
其中，$K$ 是码本中代码的总数量，$i \in {1,2,\dots,h\times w}$ 。通过量化过程，模型能够有效地压缩和表示图像的特征，并增强图像生成的多样性和准确性，从而帮助提高图像生成质量和模型效率。
#### Decoder
解码器的任务是将量化后的特征表示 $z_{q}$ 转换回高分辨率图像。解码器结构由一系列上采样器组成，每个上采样器都会将图像的高度和宽度增加一倍，从而逐步恢复原始图像的空间分辨率。具体来说，高分辨率图像 $\hat{y}$ 由量化特征表示 $z_{q}$ 通过解码器 $G$ 重建：
$$\hat{y}=G(z_{q})\approx y$$
解码器不仅需要生成高质量的图像，还要确保生成的图像在视觉上逼真和自然。
#### Discriminator

为了提高生成图像的质量，我们引入了UNet鉴别器作为判别器模块。UNet的结构包括一个对称的编码器-解码器（Encoder-Decoder）架构，并在编码器和解码器之间通过跳跃连接（Skip Connections）进行连接。UNet鉴别器的主要功能是区分生成的高分辨率图像 $\hat{y}$ 和真实的高分辨率图像 $y$。通过对抗训练，生成器不断提升其能力，以生成能够欺骗判别器的高质量图像。这种对抗机制有效地提升了生成图像的逼真度和细节还原能力。

特别是在盲超分辨率（Blind Super-Resolution）任务中，UNet鉴别器通过多尺度特征提取和高分辨率细节保留，能够更有效地处理各种退化情况，使得生成的超分辨率图像在未知降质模型下仍能保持高质量和真实感，从而显著提升盲超分辨率任务的性能。

### Training Pipeline

#### Stage 1, Pretraining of VQGAN Backbone
在这个阶段中，我们使用 HR 图像集来训练由编码器 E、离散码本 Z 和解码器 G 组成的 VQGAN  Backbone。阶段一的训练过程如图3-3所示。
为了训练Encoder和Decoder，我们用 $y$ 和 $\hat{y}$ 来计算重建损失函数，重建损失函数主要由 L1 loss和 perceptual loss组成：
$$\begin{aligned}\mathcal{L}_{rec}=\lambda_{L1}\|\hat{y}-{y}\|_1+\lambda_{per}\|\phi(\hat{y})-\phi({y})\|_2^2\end{aligned}$$
而对于Codebook，由于方程（1）中的量化操作不可微，我们采用了文献[7]中的直通梯度估计器（Straight-Through Estimator）进行训练。该估计器直接将解码器 \(G\) 的梯度复制到编码器 \(E\)，从而实现了反向传播，并允许在使用代码级损失函数 \(L_{VQ}\) 进行端到端训练。
$$\begin{aligned}\mathcal{L}_{VQ}(E,G,\mathcal{Z})=\|\operatorname{sg}[\hat{z}]-z\|_{2}^{2}+\beta\|\mathrm{sg}[z]-\hat{z}\|_{2}^{2}\end{aligned}$$
其中 sg[·] 是停止梯度操作，根据 β = 0.25。通过预训练的 VQGAN，训练集中的任何高分辨率图像 y 都可以用 Z 中相应的特征向量和解码器 G 来重建。
因此，阶段一的总损失函数定义为
$$\begin{aligned}\mathcal{L}_{stage_{1}}=\mathcal{L}_{rec}+\mathcal{L}_{VQ}\end{aligned}$$
根据[9]，其中每个损失的权重设置为：$\lambda_{L1}=\lambda_{per}=1,\beta=0.25$

#### Stage 2, Super-Resolution
在阶段二，我们使用LR和HR成对图像集来对Encoder，ConvNeXt和Discriminator来进行训练。阶段二的训练过程如图3-3所示。
在这个阶段，我们同样使用重建损失来作为损失函数的其中一部分来对Encoder，ConvNeXt进行训练。除此之外，我还添加了hinge loss作为对抗性损失。
$$\mathcal{L}_{adv}=\lambda_{adv}\sum_{i}-\mathbb{E}[D(\hat{{y}_i})]$$
因此，阶段一的总损失函数定义为
$$\begin{aligned}\mathcal{L}_{stage_{2}}=\mathcal{L}_{rec}+\mathcal{L}_{adv}\end{aligned}$$
根据[9]，其中每个损失的权重设置为：$\lambda_{L1}=1,\lambda_{adv}=0.1,\beta=0.25$
此外，用于训练discriminator的损失函数定义为：
$$L_D=\sum_{i}\{\mathbb{E}[\max(0,1-D(y_{i}))]+\mathbb{E}[\max(0,1+D(\hat{y}_{i})]\}$$