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

To address the problem of blind super-resolution with unknown degradation models, the main contributions of this study are as follows:

1. The paper propose a novel super-resolution model based on VQGAN, integrating a CNN-based ConvNeXt structure as a feature extractor to enhance the model's ability to extract features from LR images. This design significantly improves the quality of super-resolved images while ensuring performance and efficiency.
2. Various strategies are implemented to improve the utilization of the codebook within the VQGAN framework, including optimizing its capacity, improving its initialization, applying regularization techniques, and using an Exponential Moving Average (EMA) dynamic updating strategy. These strategies allow for better dynamic adjustment of the codebook during training, further enhancing the model's adaptability and generalization capability when handling diverse image content.
3. A phased training strategy is adopted: in the first phase, the encoder, codebook, and decoder are primarily trained within the VQGAN framework; in the second phase, we concentrate on training the Encoder along with the ConvNeXt feature extractor and GAN network. This approach effectively mitigates the instability of GAN training, enhancing the model's training stability and efficiency.

Experimental validation on multiple datasets demonstrates that our proposed model outperforms existing technologies in the task of image super-resolution.