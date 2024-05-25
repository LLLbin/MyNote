### 1.1 Research Background and Motivation

Image super-resolution (SR) is a significant research topic in computer vision, aiming to recover high-resolution (HR) images from low-resolution (LR) images. This technology has broad application prospects in consumer electronics, medical imaging, remote sensing and satellite imagery, video surveillance, and other fields. For example, in high-definition televisions and smartphones, super-resolution technology can significantly enhance the visual quality of images; in medical imaging, it can help doctors observe pathological details more clearly, thereby improving diagnostic accuracy. In recent years, with the development of deep learning technology, image super-resolution methods have made remarkable progress. However, existing technologies still face many challenges in practical applications. Traditional super-resolution methods perform poorly when dealing with unknown degradation processes. Therefore, there is an urgent need for a new approach to overcome these issues and enhance the practical effectiveness of image super-resolution technology.

### 1.2 Problem Definition
Traditional image super-resolution techniques typically assume that the input LR images are generated through a specific degradation model, such as bicubic downsampling. These methods perform well under controlled conditions but face numerous challenges in practical applications due to the complex and unknown nature of image degradation. LR images may be affected by various factors including blurring, noise, and different downsampling techniques, making it difficult for traditional SR methods to cope.

Blind super-resolution addresses the challenge of unknown degradation models and primarily faces the following difficulties:

- The degradation process can be caused by various factors, such as motion blur, optical blur, and noise, making it extremely challenging to accurately recover HR images from degraded LR images.
- The content and quality of LR images can vary greatly, including natural scenes, faces, text, etc., requiring the model to have strong generalization capabilities across different types of images.
- Balancing detail reconstruction and artifact suppression during the HR image recovery process is a major challenge. Over-enhancing details can introduce artifacts, whereas excessive suppression can lead to loss of detail.
- Due to the complexity of blind super-resolution tasks, training stable and high-performing models is challenging, especially when using techniques like generative adversarial networks (GANs), which can lead to inconsistent image quality during training.
### 1.3 Contributions

针对未知退化模型的盲超分辨率问题，本研究的主要贡献如下：

1. 本研究提出一种新型基于VQGAN的超分辨率模型，将基于CNN的ConvNeXt结构集成为特征提取器，增强了模型对低分辨率图像的特征提取能力，从而在保证性能和效率的同时显著提高了超分辨率图像的质量。
2. 在VQGAN的基础上结合动态更新的codebook策略（ema），在训练过程中更好地动态调整codebook，进一步增强了模型在处理多样化图像内容时的适应性和泛化能力。
3. 采用分阶段训练策略，第一阶段训练VQGAN的Encoder、Codebook和Decoder；第二阶段重点训练Encoder与ConvNeXt特征提取器及GAN网络，有效缓解了GAN训练的不稳定性，提高了模型的训练稳定性和效率。

通过在多个数据集上的实验验证，本研究提出的模型在图像超分辨率任务上的表现优于现有技术。