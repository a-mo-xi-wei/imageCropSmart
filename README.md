# image smart crop(图片智能裁剪)  

## 描述

使用 OpenCV 智能裁剪图像, 源自 `epixelic/python-smart-crop`,并进行了更多改进。

使用了https://github.com/thumbor/thumbor/wiki/Detection-algorithms 中描述的算法，但实际上结合了两种方法。我们尝试在图像上检测人脸，然后在任何情况下都检测特征。然后我们将两种结果以不同的权重结合起来，因此在这种情况下，人脸检测比特征检测强3.33倍。

## 安装

需要python-opencv，使用 `pip install python-opencv`安装依赖项

使用PIP安装命令: `pip install git+https://github.com/fizzday/imageCropSmart`

## Usage
- #### *command line*
用法： `smartcrop -W 640 -H 360 -i input.jpg -o output.jpg`

请参阅 `smartcrop --help` 

- #### *python source code*  
```python
import smartcrop

img_input = "input.jpg"
img_output = "output.jpg"
img_width = 400
img_height = 300

smartcrop.smart_crop(img_input, img_width, img_height, img_output, None)
``` 

任何情况：您可以在`./smartcrop/_init_.py`中运行代码 


## example1
- input.jpg  
    ![input.jpg](https://raw.githubusercontent.com/fizzday/imageCropSmart/master/smartcrop/input.jpg)  
    - crop  
    ```
    smartcrop -W 400 -H 300 -i input.jpg -o output.jpg
    ```
    ![output.jpg](https://raw.githubusercontent.com/fizzday/imageCropSmart/master/smartcrop/output.jpg)  
    
## example2
- input2.jpg  
    ![input2.jpg](https://raw.githubusercontent.com/fizzday/imageCropSmart/master/smartcrop/input2.jpg)  
    ```
    smartcrop -W 400 -H 300 -i input2.jpg -o output2.jpg
    ```
    ![output2.jpg](https://raw.githubusercontent.com/fizzday/imageCropSmart/master/smartcrop/output2.jpg)
## exampleCode
```python
import smartcrop
import os

src_dir = "./downloaded_images"
img_output_dir = "output"  # 存放裁剪后的图片的文件夹
img_width = 200
img_height = 200

# 创建存放输出图片的文件夹（如果不存在）
os.makedirs(img_output_dir , exist_ok = True)

# 遍历 src_dir 中的所有图片文件
for img_file in os.listdir(src_dir) :
    # 只处理图片文件，比如根据文件扩展名来过滤
    if img_file.lower().endswith(('.jpg' , '.jpeg' , '.png' , '.bmp')) :
        img_input = os.path.join(src_dir , img_file)
        img_output = os.path.join(img_output_dir , img_file)

        # 调用 smartcrop 函数裁剪图片
        smartcrop.smart_crop(img_input , img_width , img_height , img_output , None)
        print(f"裁剪完成: {img_input} -> {img_output}")

```

