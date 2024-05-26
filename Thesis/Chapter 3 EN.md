### Overview of Proposed Model

This paper proposes a super-resolution model based on the VQGAN architecture, combined with a ConvNeXt feature extraction module. The overall network architecture, as shown in Figure 3-1, primarily consists of the following five components: the Encoder, the ConvNeXt feature extractor, the Codebook, the Decoder, and the Discriminator.

#### Encoder

The primary task of the encoder is to extract and compress features from the input low-resolution images. The encoder structure consists of multiple downsamplers, which convert the low-resolution image into a compact feature representation $\hat{x}$. Each downsampler reduces the height and width of the image by half. Specifically, given an input image \(x \in \mathbb{R}^{H \times W \times 3}\), the VQ-encoder processes it to output a feature representation \(\hat{x} \in \mathbb{R}^{\frac{H}{2^n} \times \frac{W}{2^n} \times n_{\hat{x}}}\). This feature representation not only retains essential information from the image but also reduces the spatial dimensions of the features, laying the foundation for subsequent feature processing and quantization.

#### ConvNeXt

To further enhance feature extraction capabilities, we introduced the ConvNeXt module based on Convolutional Neural Networks (CNN) after the encoder. The structure of the ConvNeXt module is shown in Figure 3-2 and consists of the following three parts:

- **Stem Layer**: This layer uses a `4x4` convolution kernel for downsampling, significantly reducing the size of the input image, thereby decreasing computational complexity and improving the speed and efficiency of subsequent modules. Additionally, LayerNorm is introduced for normalization, which helps improve the stability of network training and model performance.
- **Four-Stage Feature Extraction (Stages)**: Each stage begins with a downsampling layer that further reduces the size of the feature maps. Each downsampling layer typically uses a `2x2` convolution kernel with a stride of 2. Following this is a series of convolutional blocks (Blocks), where each block employs Depthwise Convolution (DwConv) technology to extract spatial features. These features are then arranged and normalized to enhance numerical stability during training. Finally, two linear layers are used for feature transformation, connected by the GELU activation function. At the end of each convolutional block, the processed features are directly added to the block inputs, forming skip connections to introduce residual learning. Additionally, DropPath, a type of stochastic depth technique, is added to enhance the model's generalization capability and robustness.
- **Upsampler Layers**: PixelShuffle technology is used for upsampling to meet the input size requirements of the codebook.

The ConvNeXt module uses convolution operations to extract richer image features while preserving spatial information, thereby improving the model's ability to capture features from low-resolution images and producing clearer and more detailed high-resolution images.