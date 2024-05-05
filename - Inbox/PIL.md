##### 0. 获取图像信息
```python
# 获取图像尺寸
print(img.size)
# 获取图像模式
print(img.mode)
# 获取图像格式
print("Format:", img.format)
```
##### 1. 打开和保存图像
```python
from PIL import Image

# 打开图像
img = Image.open("path/to/image.jpg")
# 保存图像
img.save("path/to/output.jpg", format='JPEG')
```

##### 2. 图像转换
```python
# 转换图像到灰度模式
# 'L' 表示灰度模式
gray_img = img.convert('L')

# 转换图像到RGB模式
# 'RGB' 用于全彩色图像（红，绿，蓝）
rgb_img = img.convert('RGB')

# 转换图像到RGBA模式
# 'RGBA' 添加了透明通道（红，绿，蓝，透明度）
rgba_img = img.convert('RGBA')

# 转换图像到1位像素模式
# '1' 二值图像，即像素非黑即白
one_bit_img = img.convert('1')
```

##### 3. 图像大小和裁剪
```python
# 改变图像大小
resized_img = img.resize((200, 200))
# 裁剪图像
cropped_img = img.crop((100, 100, 400, 400))
```

##### 4. 图像旋转和翻转
```python
# 旋转图像90度
rotated_img = img.rotate(90, expand=True)
# 水平翻转图像
flipped_img = img.transpose(Image.FLIP_LEFT_RIGHT)
```

##### 5. 图像合并和分割
```python
# 分割图像为单独的通道
r, g, b = img.split()
# 合并图像通道
merged_img = Image.merge("RGB", (b, g, r))
```

##### 6. 图像滤镜和增强
```python
from PIL import ImageFilter, ImageEnhance

# 应用模糊滤镜
blurred_img = img.filter(ImageFilter.BLUR)
# 增强图像对比度
enhancer = ImageEnhance.Contrast(img)
enhanced_img = enhancer.enhance(2.0)
```

##### 7. 绘制工具
```python
from PIL import ImageDraw

# 在图像上绘制
draw = ImageDraw.Draw(img)
draw.line((0, 0, 100, 100), fill="blue")
draw.text((10, 10), "Hello World", fill="green")
```