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

由于openCV使用的是gbk编码，而py3使用的是utf-8编码所以需要先将编码转换为gbk编码

```python
# 将utf-8转化为gbk
def zh_ch(string):    
	return string.encode("gbk").decode(errors="ignore")
```

### 将图像转化为灰度图像

```python
```

