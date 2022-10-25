## Install OpenCV

```bash
pip3 install opencv-contrib-python -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 基本操作

### 读取并显示图像

```python
# 导包并重命名
import cv2 as cv
# cv.imread(图像路径, 1/0/-1)
# 1  cv.IMREAD * COLOR：    (默认参数)以彩色模式加载图像，任何图像的透明度都将被忽略
# 0  cv.IMREAD * GRAYSCALE：以灰度模式加载图像
# -1 cv.IMREAD_UNCHANGED：  包括alpha通道的加载图像模式
img = cv2.imread('images/1.png', 0)
# 展示图像
cv2.imshow("myWindow", img)
# 显示图形的时间(ms)
# 设置waitKey(0) , 则表示程序会无限制的等待用户的按键事件, 一般在 imgshow 的时候, 如果设置 waitKey(0), 代表按任意键继续
cv2.waitKey(0)
# 销毁窗口
cv2.destroyAllWindows()
```

### 解决窗口标题中文乱码问题

由于openCV使用的是gbk编码，而py3使用的是utf-8编码所以需要先将编码转换为gbk编码， **并不万能，建议用英文**

```python
# 将utf-8转化为gbk
def zh_ch(string):    
	return string.encode("gbk").decode(errors="ignore")
```

### 将原图转化为灰度图像

```python
# 将原图像转化为灰度图像
img_gray = cv.cvtColor(img, cv.COLOR_RGB2GRAY)
cv.imshow('Gray Image', img_gray)
```

### 将灰度图像转化为二值图

```python
# 将灰度图转化为二值图像
ret, img_thresh = cv.threshold(img_gray, 127, 255, cv.THRESH_BINARY)
cv.imshow('Thresh Image', img_thresh)
```

### 对二值图进行轮廓提取和轮廓绘制

```python
# 轮廓提取
contours, hierarchy = cv.findContours(img_thresh, cv.RETR_TREE, cv.CHAIN_APPROX_SIMPLE)
# 轮廓绘制
cv.drawContours(img, contours, -1, (0, 0, 255), 3)
cv.namedWindow('Contour Image', 0)
cv.imshow('Contour Image', img)
```

### 完整代码

```python
import cv2 as cv
import numpy as np

if __name__ == "__main__":
    # 图片路径
    img_path = './images/1.png'
    # 读入图片(彩色)
    img = cv.imread(img_path, 1)
    # 获取图片宽和高
    width, height = img.shape[:2][::-1]
    # 将图片缩小便于显示观看
    img = cv.resize(img, (int(width*0.8), int(height*0.8)),
                    interpolation=cv.INTER_CUBIC)
    print("img_reisze shape:{}".format(np.shape(img)))
    cv.imshow('Original Image', img)
    # 将原图像转化为灰度图像
    img_gray = cv.cvtColor(img, cv.COLOR_RGB2GRAY)
    cv.imshow('Gray Image', img_gray)
    # 将灰度图转化为二值图像
    ret, img_thresh = cv.threshold(img_gray, 127, 255, cv.THRESH_BINARY)
    cv.imshow('Thresh Image', img_thresh)
    # 轮廓提取
    contours, hierarchy = cv.findContours(
        img_thresh, cv.RETR_TREE, cv.CHAIN_APPROX_SIMPLE)
    # 轮廓绘制
    cv.drawContours(img, contours, -1, (0, 0, 255), 3)
    cv.namedWindow('Contour Image', 0)
    cv.imshow('Contour Image', img)
    # 目标框出

    cv.waitKey()
```

