

### P1

图像超分辨率（SR）是计算机视觉领域的一个重要的研究课题，旨在从低分辨率（LR）图像恢复高分辨率（HR）图像。目前人们会因为图像采集设备的限制，会采集到细节丢失，视觉效果差的低分辨率图像。超分辨率技术就是要解决这些问题的，要做的不仅仅是指把图像的尺寸放大，更重要的是提升图像的清晰度，突出图像中的纹理和细节，改善视觉体验。


目前SISR通常假设输入的低分辨率图像是通过特定的退化模型生成的，例如双三次插值降采样。这些方法在基于已知退化模型的方法在特定情况下表现良好，但实际中低分辨率图像可能受到多种因素的影响，传统的超分辨率方法难以应对这些情况。

针对未知退化模型的图像进行超分辨率称之为盲超分辨率。盲超分辨率的难点主要体现在以下方面：

- 图像的退化过程可能由多种因素造成，如运动模糊、光学模糊、噪声等。这些未知且复杂的退化过程使得从低分辨率图像中准确恢复出高分辨率图像变得极为困难。
- 低分辨率图像的内容和质量可能差别非常大，包括自然场景、人脸、文本等不同类型的图像。这要求模型具有较强的泛化能力，能够在不同类型的图像上都表现出色。
- 在恢复高分辨率图像的过程中，如何在重建细节和抑制伪影之间取得平衡是一大难点。过度增强细节可能引入伪影，而过度抑制伪影又可能导致细节丢失。
- 由于盲超分辨率任务的复杂性，训练稳定且性能优异的模型具有一定难度。特别是在使用生成对抗网络（GAN）等方法时，模型训练过程中容易出现不稳定现象，导致生成图像质量不一致。

### P2

- **Integration of ConvNeXt with VQGAN for Enhanced Feature Extraction**: The paper proposes a novel super-resolution model based on VQGAN, integrating a CNN-based ConvNeXt structure as a feature extractor. This design significantly improves the quality of super-resolved images while ensuring performance and efficiency.
    
- **Optimized Codebook Utilization**: Various strategies are implemented to improve the utilization of the codebook within the VQGAN framework, including optimizing its capacity, improving its initialization, and using an Exponential Moving Average (EMA) dynamic updating strategy. These strategies allow for better dynamic adjustment of the codebook during training, further enhancing the model's adaptability and generalization capability when handling diverse image content.
    
- **Phased Training Strategy**: A phased training strategy is adopted: in the first phase, the encoder, codebook, and decoder are primarily trained within the VQGAN framework; in the second phase, we concentrate on training the Encoder along with the ConvNeXt feature extractor and GAN network. This approach effectively mitigates the instability of GAN training, enhancing the model's training stability and efficiency.



Propose a novel super-resolution model based on VQGAN and ConvNeXt.

Optimized Codebook Utilization in VQGAN

Phased Training Strategy



我们在盲超分辨率任务中使用是VQGAN（Vector Quantized Generative Adversarial Network）的原因在于其强大的表征能力和动态调整的量化码本。通过量化学习复杂的高维图像表示，VQGAN能够捕捉并重建出细致的图像细节，适应多种未知的退化因素。此外，VQGAN结合了生成对抗网络（GAN）的优势，通过对抗训练提高了生成图像的质量，从而在处理复杂和多变的退化情况下生成高质量的超分辨率图像。