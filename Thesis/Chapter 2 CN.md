### 2.1 Non-blind Single Image Super-Resolution

近年来，通过深度学习在单图像超分辨率（SISR）任务中取得了重大进展。 Dong 等人\cite{dong2014learning} 提出的开创性 SRCNN，使用卷积神经网络 (CNN) 来放大和细化低分辨率 (LR) 图像，生成高分辨率 (HR) 图像。 SRCNN开创了深度学习在SISR领域的应用，并带动了后续的广泛研究。

VDSR\cite{kim2016accurate} 和 IRCNN\cite{zhang2017learning} 以 SRCNN 为基础，通过增加网络深度和合并残差连接来增强超分辨率性能。残差连接的引入改进了梯度传播，解决了深度网络训练中的梯度消失问题。随后，Tong等人\cite{tong2017image}通过引入密集连接进行了进一步的改进。后来，RDN\cite{zhang2018residual}通过使用更深更宽的网络来优化网络架构，结合残差密集块来增强特征提取能力。此外，EPSCN\cite{shi2016real}提出了高效的子像素卷积层和像素洗牌，以有效实现图像上采样并显着增强超分辨率模型的性能。此外，Chen 等人\cite{chen2022multi} 和 Huang 等人\cite{huang2022single} 利用基于 CNN 的多尺度特征提取网络来捕获更多图像信息以实现图像超分辨率。

除了网络深度和结构的改进之外，SISR还引入了注意力机制，以增强对重要特征的关注并提高图像重建质量。例如，RCAN\cite{zhang2018image}结合了信道注意机制，自适应调整每个信道的权重以增强细节处理，而EMAN\cite{zhang2022enhanced}添加像素注意机制和边缘损失函数以提高边缘区域的学习能力。
### 2.2 Blind Single Image Super-Resolution

随着单图像超分辨率（SISR）研究的成熟，最近的工作已经转向更具挑战性的盲 SISR 任务，该任务处理未知的退化模型。目前针对盲 SISR 的解决方案主要分为隐式方法和显式方法。隐式方法从现实世界的低分辨率 (LR) 图像中学习退化模型。这些方法通常采用无监督学习技术\cite{wang2021unsupervised, cornillere2019blind, zhang2021blind, kim2020dual}来捕获图像退化的复杂特征。相比之下，显式方法通过手动设计退化过程来生成“真实”LR 图像，如 BSRGAN 和 Real-ESRGAN 所示。如果设计良好，显式方法通常比隐式方法在盲 SISR 中实现更好的视觉质量。

隐式和显式方法都依赖于变分自动编码器（VAE）\cite{kingma2013auto}或生成对抗网络（GAN）\cite{goodfellow2014generative}的生成能力来生成高质量的纹理。因此，最近对盲 SISR 的研究主要集中在基于 VAE 或 GAN 的模型上。首先，莱迪格等人。提出了SRGAN\cite{ledig2017photo}，它是第一个将GAN应用于超分辨率任务，生成逼真的高分辨率（HR）图像。在此基础上，王等人。引入了ESRGAN\cite{wang2018esrgan}，结合了残差密集块和相对均方误差损失，显着增强了图像细节和视觉质量。随后，张等人。设计了 BSRGAN\cite{zhang2021designing}，它模拟各种退化过程以生成用于训练的真实 LR 图像。基于此，王等人。结合现实世界的退化模型提出了 Real-ESRGAN\cite{wang2021real}，它可以处理复杂的现实世界退化并产生更真实的 HR 图像。最近，埃塞尔等人。结合了VAE和GAN的优点，利用矢量量化（VQ）设计了VQGAN\cite{esser2021taming}，它在自然图像合成和细节保留方面表现出色，为盲SISR提供高质量的先验。在此基础上，Chen等人使用swin