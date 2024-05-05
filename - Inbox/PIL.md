##### 0. 打开和保存图像
```python
from PIL import Image

# 打开图像
# Image.open函数用于加载图像文件，支持多种格式如JPEG, PNG等
# 参数是图像文件的路径
img = Image.open("path/to/image.jpg")

# 保存图像
# img.save函数用于将图像保存到文件
# 参数1: 文件的保存路径
# 参数2: format指定保存的图像格式，例如'JPEG', 'PNG'等
img.save("path/to/output.jpg", format='JPEG')

# 另存为PNG格式
# 如果不指定format，Pillow会根据文件扩展名自动推断格式
img.save("path/to/output.png")

# 保存图像时指定压缩质量
# quality参数可用于JPEG格式，范围从1（最差质量，最小文件）到95（最佳质量，较大文件）
img.save("path/to/output_quality.jpg", 'JPEG', quality=85)

# 保存为透明PNG
# 首先确保图像是RGBA模式，然后保存为PNG
if img.mode != 'RGBA':
    img = img.convert('RGBA')
img.save("path/to/output_transparent.png", 'PNG')

# 保存时指定优化参数
# optimize参数在保存JPEG和PNG时可用，用于进一步压缩文件大小
img.save("path/to/output_optimized.png", 'PNG', optimize=True)
```

##### 1. 获取图像信息
```python
# 获取图像尺寸
# size属性返回一个元组，包含图像的宽度和高度（width, height）
print("Size:", img.size)

# 获取图像模式
# mode属性返回一个字符串，描述图像的颜色组成模式，常见的如 'RGB'、'L' (灰度) 等
print("Mode:", img.mode)

# 获取图像格式
# format属性返回图像的格式，如 'JPEG'、'PNG' 等，如果图像不是从文件读取的，则可能为 None
print("Format:", img.format)
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
# resize函数用于调整图像的尺寸
# 参数为一个元组，指定新的宽度和高度
resized_img = img.resize((200, 200))

# 保持比例缩放图像
# thumbnail方法调整图像大小，保持原有宽高比，尺寸不会超过指定的宽度和高度
img.thumbnail((200, 200))  # 直接修改img对象

# 裁剪图像
# crop函数用于裁剪图像
# 参数是一个四元组，定义裁剪区域的左、上、右、下坐标
cropped_img = img.crop((100, 100, 400, 400))
```

##### 4. 图像旋转和翻转
```python
# 旋转图像
# rotate方法用于旋转图像
# 参数1: angle指定旋转的角度，正值为逆时针旋转，负值为顺时针旋转
# 参数2: expand如果设置为True，会扩展图像的尺寸以适应整个旋转后的图像
rotated_img = img.rotate(90, expand=True)

# 逆时针旋转180度，不扩展图像
rotated_img_180 = img.rotate(180)

# 水平翻转图像
# transpose方法用于翻转图像
# Image.FLIP_LEFT_RIGHT为水平翻转
flipped_img = img.transpose(Image.FLIP_LEFT_RIGHT)

# 垂直翻转图像
# Image.FLIP_TOP_BOTTOM为垂直翻转
flipped_img_vertical = img.transpose(Image.FLIP_TOP_BOTTOM)

# 旋转并保持原始尺寸
# expand设为False时，旋转的图像会被裁剪到原图大小
rotated_no_expand = img.rotate(45, expand=False)
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
from PIL import 

# 应用模糊滤镜
# BLUR是一个简单的平均模糊滤镜
blurred_img = img.filter(ImageFilter.BLUR)

# 应用更强的高斯模糊滤镜
# GAUSSIAN_BLUR用于创建高斯模糊效果，可以传入radius参数来指定模糊半径
gaussian_blur_img = img.filter(ImageFilter.GaussianBlur(radius=5))

# 应用锐化滤镜
# SHARPEN滤镜增加图像的清晰度
sharpened_img = img.filter(ImageFilter.SHARPEN)

# 应用边缘增强滤镜
# EDGE_ENHANCE强调图像边缘，使边缘更清晰
edge_enhanced_img = img.filter(ImageFilter.EDGE_ENHANCE)

# 应用细节增强滤镜
# DETAIL滤镜增强图像细节
detailed_img = img.filter(ImageFilter.DETAIL)

# 增强图像对比度
# Contrast创建对比度增强对象，enhance方法用于应用增强效果
# 参数factor > 1增加对比度，factor = 1原始图像，factor < 1减少对比度
enhancer = ImageEnhance.Contrast(img)
enhanced_img = enhancer.enhance(2.0)  # 对比度提高2倍

# 增强图像亮度
# Brightness同样创建亮度增强对象，enhance方法应用亮度调整
brightness_enhancer = ImageEnhance.Brightness(img)
brightened_img = brightness_enhancer.enhance(1.5)  # 亮度提高50%
```

##### 7. 绘制工具
```python
# 创建一个绘制对象
draw = ImageDraw.Draw(img)

# 绘制线条
# line接收开始和结束坐标，以及颜色填充
draw.line((0, 0, 100, 100), fill="blue", width=3)

# 绘制文本
# text接收位置坐标，文本内容和填充颜色
draw.text((10, 10), "Hello World", fill="green")

# 绘制矩形
# rectangle接收左上角和右下角坐标，可选的填充和轮廓颜色
draw.rectangle((50, 50, 150, 100), fill="red", outline="black")

# 绘制椭圆
# ellipse接收左上角和右下角坐标，定义椭圆边界，可选的填充和轮廓颜色
draw.ellipse((200, 50, 300, 150), fill="yellow", outline="black")

# 绘制圆弧
# arc接收左上角和右下角坐标，起始角度和结束角度，以及颜色填充
draw.arc((200, 200, 300, 300), start=0, end=180, fill="black")

# 绘制多边形
# polygon接收点的列表，可选的填充和轮廓颜色
draw.polygon([(400, 200), (300, 300), (500, 300)], fill="purple", outline="white")
```