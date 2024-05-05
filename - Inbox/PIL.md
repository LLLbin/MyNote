##### 1. 打开和保存图像
```python
# 打开图像
from PIL import Image
img = Image.open("path/to/image.jpg")
# 保存图像
img.save("path/to/output.jpg", format='JPEG')
```

##### 2. 图像转换
```python
# 转换图像到灰度模式
img = img.convert('L')
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

##### 8. 获取图像信息
```python
# 获取图像尺寸
print(img.size)
# 获取图像模式
print(img.mode)
```

以上就是一些基本的PIL库操作，每个示例都可以直接运行，只需要提供正确的文件路径和参数。