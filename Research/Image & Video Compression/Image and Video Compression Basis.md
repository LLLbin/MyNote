# 1. INTRO TO IMAGE COMPRESSION AND INFORMATION
# 1.1 Type of Digital Image
| type               | bits     | meaning                              |
| ------------------ | -------- | ------------------------------------ |
| Binary image       | 1        | black or while                       |
| Grayscale image    | 8        | black to while                       |
| Pseudo-color image | 8        | a color chosen from a large universe |
| True color image   | 24       | (R, G, B)                            |
| Deep color image   | 30/36/48 | (R, G, B)                            |
## 1.2 Data Compression
### 1.2.1 Define 
- The process of reducing the amount of ==data== required to represent a given quantity of ==information==.
### 1.2.2 Compression Ratio: 
	$C_R=\frac{n_1}{n_2}$
	$n_1$: ==before== compression 
	$n_2$: ==after== compression 
## 1.3 Data Redundancies
### 1.3.1 Coding redundancy (lossless)
- ==Average number of bits representing each pixel== 
	- $L_{avg} = \sum_{k=0}^{L-1} l(r_k) p_r(r_k)$
	- $l(r_k)$: number of bits
	- $p_r(r_k)$: probability that $r_k$ occurs
	![[Pasted image 20240213232135.png]]
- ==Variable-length coding (VLC)==
	- Assign fewer bits to more probable graylevels. The operation is reversible and results in losslesscompression
	- ==Huffman Coding==, ==Arithmetic Coding==
	- Coding redundancy can be reduced by VLC
### 1.3.2 Interpixel redundancy (lossless)
- Value of any given pixel can be reasonably predicted from the values of its neighbors. 
- ==Run-length coding (RLC)==
	- since binary image contains many regions of constant intensity, we map pixels along each scan line into sequence of pairs (g1, r1), (g2, r2)
	- $g_i$ = ith gray level 
	- $r_i$ = run length of the ith run
### 1.3.3 Psychovisual redundancy (lossy)
- Certain information has less relative importance in visual processing
- ==Quantization==
	- mapping a broad range of input values to a limited number of output values.
	- $q(x) = \left\lfloor  \frac{x}{Q}  \right\rfloor*Q$
## 1.4 Fidelity Criteria
$e_{rms} = \left[ \frac{1}{MN} \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} \left( \hat{f}(x, y) - f(x, y) \right)^2 \right]^{1/2}$
$SNR_{ms} = \frac{\sum_{x=0}^{M-1} \sum_{y=0}^{N-1} \hat{f}(x, y)^2}{\sum_{x=0}^{M-1} \sum_{y=0}^{N-1} \left( \hat{f}(x, y) - f(x, y) \right)^2}$
$PSNR=\frac{255^2}{\sum_{x=0}^{M-1} \sum_{y=0}^{N-1} \left( \hat{f}(x, y) - f(x, y) \right)^2}$
## 1.5 Information Theory
- Self-information fo random event E with probability P(E)
	- $I(E) = \log_{2} \frac{1}{P(E)} = -\log_{2} P(E)$
- Entropy
	- $H(z) = \sum_{j=1}^{J} P(a_j)I(a_j) = -\sum_{j=1}^{J} P(a_j) \log_{2} P(a_j)$
- Conditional Entropy
	- $H(z | v) = -\sum_{b_k \in V} \sum_{a_j \in Z} P(a_j, b_k) \log_{2} P(a_j | b_k)$
	- $H(v | z) = -\sum_{a_j \in Z} \sum_{b_k \in V} P(a_j, b_k) \log_{2} P(b_k | a_j)$
- Joint Entropy
	- $H(z, v) = \sum_{a_j \in z} \sum_{b_k \in v} P(a_j, b_k) \log_{2} P(a_j, b_k)$
	- $H(z , v) = H(z) + H(v | z)$
	- $H(z , v) = H(v) + H(z | v)$
- Relative Entropy
	- $D(p \| q) = \sum_{a_j \in z} p(a_j) \log_{2} \frac{p(a_j)}{q(a_j)}$
- Cross Entropy
	- $H_{q}(p) = -\sum_{a_j \in z} p(a_j) \log_{2} q(a_j)$
	- $H_{q}(p)=H(p)+D(p\|q)$
- Mutual Information
	- $I(z, v) = \sum_{a_j \in z} \sum_{b_k \in v} p(a_j, b_k) \log_{2} \frac{p(a_j, b_k)}{p(a_j) p(b_k)}$
	- $I(z, v) = H(z) - H(z | v)$
	- $I(z, v) = H(z) + H(v) - H(z, v)$
    ![[Pasted image 20240214010655.png]]

# 2. ENTROPY CODING
## 2.1 Intro
- No loss of information during compression process. (==lossless==)
- Reduce coding redundancies & interpixel redundancies.
- Low compression ratio: typically 2:1 to 15:1.
## 2.2 Huffman Coding (VLC)
![[Pasted image 20240214013035.png]]
## 2.3 Golomb Coding (VLC)
### 2.3.1 Normal
![[Pasted image 20240214013232.png]]
![[Pasted image 20240214013248.png]]
### 2.3.2 Exponential
![[Pasted image 20240214013348.png]]
![[Pasted image 20240214013437.png]]
## 2.4 Arithmetic Coding
![[Pasted image 20240214013543.png]]
![[Pasted image 20240214013631.png]]
## 2.5 LZW Coding
- Lempel-Ziv-Welch (LZW) coding assigns fixed-length code words to variable length sequences of source symbols but requires no a priori knowledge of the probability of occurrence of symbols to be encoded
- It also tracks image’s interpixel redundancies
- It also used in text compression
![[Pasted image 20240214013841.png]]
## 2.6 Bit-Plane Coding
- Decompose a multilevel (grayscale or color) image into a series of binary images and compress each binary image
- It reduces interpixel redundancy
- Each bit plane is constructed by setting its pixels equal to the value of the appropriate bits
- Disadvantage: small change of gray level can have large impact on bit planes (hence, one way is to use Gray code)
- Higher order bit-planes are far less complex
## 2.7 Lossless Predictive Coding
![[Pasted image 20240214014358.png]]
![[Pasted image 20240214014410.png]]
![[Pasted image 20240214014607.png]]
## 2.8 Symbol-Based Coding
![[Pasted image 20240214014711.png]]
