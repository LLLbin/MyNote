### 1.1 Research Background and Motivation

图像超分辨率（Super-Resolution, SR）是计算机视觉中的一个重要研究课题，旨在从低分辨率（Low-Resolution, LR）图像恢复出高分辨率（High-Resolution, HR）图像。这项技术在消费电子产品、医学影像、遥感与卫星影像、视频监控等领域具有广泛的应用前景。例如，在高清电视和智能手机中，超分辨率技术可以显著提升图像的视觉效果；在医学影像中，它可以帮助医生更清晰地观察病变细节，提高诊断的准确性。近年来，随着深度学习技术的发展，图像超分辨率方法取得了显著进展。然而，现有技术在实际应用中仍存在诸多挑战。传统的超分辨率方法在处理未知降解过程时表现不佳。因此，迫切需要一种新的方法来克服这些问题，提升图像超分辨率技术的实际应用效果。
### 1.2 Problem Definition
目前传统的图像超分辨率方法通常假设输入的低分辨率图像是通过特定的退化模型生成的，例如双三次插值降采样。这意味着我们对图像的退化过程有明确的了解。传统的图像超分辨率方法在基于已知退化模型的方法在特定情况下表现良好，但在实际应用中仍存在诸多问题，因为图像的降解过程通常是复杂且未知的。低分辨率图像可能受到多种因素的影响，如模糊、噪声和不同的降采样方法等，传统的超分辨率方法难以应对这些情况。

针对未知退化模型的图像进行超分辨率称之为盲超分辨率。盲超分辨率的难点主要体现在以下方面：

- 图像的退化过程可能由多种因素造成，如运动模糊、光学模糊、噪声等。这些未知且复杂的退化过程使得从低分辨率图像中准确恢复出高分辨率图像变得极为困难。
- 低分辨率图像的内容和质量可能差别非常大，包括自然场景、人脸、文本等不同类型的图像。这要求模型具有较强的泛化能力，能够在不同类型的图像上都表现出色。
- 在恢复高分辨率图像的过程中，如何在重建细节和抑制伪影之间取得平衡是一大难点。过度增强细节可能引入伪影，而过度抑制伪影又可能导致细节丢失。
- 由于盲超分辨率任务的复杂性，训练稳定且性能优异的模型具有一定难度。特别是在使用生成对抗网络（GAN）等方法时，模型训练过程中容易出现不稳定现象，导致生成图像质量不一致。
### 1.3 Contributions

针对未知退化模型的盲超分辨率问题，本研究的主要贡献如下：

1. 本研究提出了一种新的基于VQGAN的超分辨率模型，在VQGAN的架构设计上添加了基于CNN的特征提取器，提升模型对于低分辨率图像的特征提取能力。此外，我还引入了注意力模块进行特征融合，将预训练的Encoder输出与CNN特征提取器的输出进行融合。这一设计提高了模型对低分辨率图像细节的捕捉能力，从而提升了超分辨率图像的质量。
2. 本研究在VQGAN的基础上结合了一种动态更新的codebook策略，通过在训练过程中对codebook进行更新，进一步增强了模型在处理多样化图像内容时的适应性和泛化能力。
3. 本研究在训练过程中采用了分阶段训练策略。在第一阶段，主要训练VQGAN中的Encoder、Codebook和Decoder；在第二阶段，训练额外的CNN特征提取器和注意力融合模块。这样的方法有效缓解了GAN训练的不稳定性，提高了模型训练的稳定性和效率。

通过在多种数据集上的实验验证，结果表明，本研究提出的模型在图像超分辨率任务中取得了优于现有方法的效果。


### 1.1 Research Background and Motivation

Image super-resolution (SR) is a significant research topic in computer vision, aiming to recover high-resolution (HR) images from low-resolution (LR) images. This technology has broad application prospects in consumer electronics, medical imaging, remote sensing and satellite imagery, video surveillance, and other fields. For example, in high-definition televisions and smartphones, super-resolution technology can significantly enhance the visual quality of images; in medical imaging, it can help doctors observe pathological details more clearly, thereby improving diagnostic accuracy. In recent years, with the development of deep learning technology, image super-resolution methods have made remarkable progress. However, existing technologies still face many challenges in practical applications. Traditional super-resolution methods perform poorly when dealing with unknown degradation processes. Therefore, there is an urgent need for a new approach to overcome these issues and enhance the practical effectiveness of image super-resolution technology.

### 1.2 Problem Definition
Traditional image super-resolution methods typically assume that the input low-resolution images are generated through specific degradation models, such as bicubic downsampling. This implies that the degradation process of the images is well understood. While traditional super-resolution methods based on known degradation models perform well in certain scenarios, they still face numerous issues in practical applications, as the degradation process of images is often complex and unknown. Low-resolution images may be affected by various factors, such as blur, noise, and different downsampling methods, making it difficult for traditional super-resolution methods to handle these situations effectively.

Super-resolution of images with unknown degradation models is referred to as blind super-resolution. The challenges of blind super-resolution are mainly reflected in the following aspects:

- The degradation process of images can be caused by multiple factors, such as motion blur, optical blur, and noise. These unknown and complex degradation processes make it extremely difficult to accurately recover high-resolution images from low-resolution images.
- The content and quality of low-resolution images can vary significantly, including different types of images such as natural scenes, faces, and text. This requires the model to have strong generalization capabilities to perform well on different types of images.
- In the process of recovering high-resolution images, balancing detail reconstruction and artifact suppression is a major challenge. Excessive detail enhancement may introduce artifacts, while excessive suppression of artifacts may lead to loss of details.
- Due to the complexity of blind super-resolution tasks, it is challenging to train stable and high-performance models. Particularly when using methods such as Generative Adversarial Networks (GANs), the training process can be unstable, leading to inconsistent image quality.

### 1.3 Contributions

To address the problem of blind super-resolution with unknown degradation models, the main contributions of this study are as follows:

1. This study proposes a novel super-resolution model based on VQGAN, incorporating a CNN-based feature extractor into the VQGAN architecture to enhance the model's ability to extract features from low-resolution images. Additionally, an attention module is introduced to perform feature fusion, integrating the outputs of the pre-trained encoder and the CNN feature extractor. This design improves the model's capability to capture details in low-resolution images, thereby enhancing the quality of the super-resolved images.
2. A dynamic codebook updating strategy is integrated into the VQGAN framework. By updating the codebook during the training process, the model's adaptability and generalization ability when dealing with diverse image content are further enhanced.
3. A staged training strategy is employed in the training process. In the first stage, the encoder, codebook, and decoder of VQGAN are primarily trained. In the second stage, the additional CNN feature extractor and the attention fusion module are trained. This method effectively alleviates the instability issues commonly encountered in GAN training, improving the stability and efficiency of the model training process.