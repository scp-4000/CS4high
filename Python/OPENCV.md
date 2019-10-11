#

```

```
## 平滑圖像
```
學習目標：
1、使用各種低通濾波器模糊圖像
2、將定制濾鏡應用於圖像（2D卷積）
https://blog.csdn.net/songchunxiao1991/article/details/80229351
```
#### 二維卷積（圖像過濾）
```
#coding:utf8
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('F:/lena.jpg', 0)
kernel = np.ones((5, 5), np.float32)/25
dst = cv2.filter2D(img, -1, kernel)
 
cv2.imshow('original', img)
cv2.imshow('result', dst)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
#### 2、圖像模糊（圖像平滑）
```
# 平均
#coding:utf8
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('F:/lena.jpg', 0)
blur = cv2.blur(img, (5, 5))
 
cv2.imshow('original', img)
cv2.imshow('result', blur)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```
#高斯濾波

#coding:utf8
import cv2
img = cv2.imread('F:/lena.jpg', 0)
blur = cv2.GaussianBlur(img,(5,5),0)
 
cv2.imshow('original', img)
cv2.imshow('result', blur)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```
#中值濾波

#coding:utf8
import cv2
img = cv2.imread('F:/lena.jpg', 0)
median = cv2.medianBlur(img,5)
 
cv2.imshow('original', img)
cv2.imshow('result', median)
cv2.waitKey(0)
cv2.destroyAllWindows(
```

```
# 雙邊濾波Bilateral Filter
#coding:utf8
import cv2
img = cv2.imread('F:/lena.jpg', 0)
blur = cv2.bilateralFilter(img,9,75,75)
 
cv2.imshow('original', img)
cv2.imshow('result', blur)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
###

OpenCV提供三種類型的梯度濾波器或高通濾波器，Sobel，Scharr和Laplacian

```
#coding:utf8
 
import cv2
import numpy as np
from matplotlib import pyplot as plt
 
img = cv2.imread('F:/lena.jpg',0)
 
laplacian = cv2.Laplacian(img,cv2.CV_64F)
sobelx = cv2.Sobel(img,cv2.CV_64F,1,0,ksize=5)
sobely = cv2.Sobel(img,cv2.CV_64F,0,1,ksize=5)
 
plt.subplot(2,2,1),plt.imshow(img,cmap = 'gray')
plt.title('Original'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,2),plt.imshow(laplacian,cmap = 'gray')
plt.title('Laplacian'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,3),plt.imshow(sobelx,cmap = 'gray')
plt.title('Sobel X'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,4),plt.imshow(sobely,cmap = 'gray')
plt.title('Sobel Y'), plt.xticks([]), plt.yticks([])
 
plt.show()
```
### openCV-python實現幻燈片漸變效果
```
https://blog.csdn.net/sh39o/article/details/79585191

漸變效果實際上是兩張圖片的加權疊加，
new image = alpha * image 1 + ( 1 - alpha ) *image 2
就可以得到一張同時含有兩張照片的合成圖。

當alpha=1時，新圖像就為image 1，
當alpha=0時相反，
實現圖片的漸變效果需要將alpha連續的從1變到0。 
opencv提供了addWeighted函數實現該功能

工具： Python3,  cv2,  os
實現流程：
    1. 使用os.chdir切換目錄，並使用os.listdir得到檔列表。
    2. 使用cv2.imread打開兩張圖，並resize到統一的大小。
    3. 將權值設置為隨著時間緩慢變化。
    4. 使用cv2.addWeighted將兩張圖加權相加。
    
result = cv2.addWeighted(src1, alpha, src2, beta, gamma, dst=None, dtype=None)   

    src1 和 src2為兩張圖片檔，這裡需要src1和src2為同一大小，alpha和beta為權值，gamma為透明度。
```

```

import cv2
import os
 
WAIT = 3000
os.chdir('/Users/mac/Pictures/Vincent')
file_list = os.listdir()
 
for i in range(len(file_list) -1):
    img1 = cv2.imread(file_list[i  ])
    img2 = cv2.imread(file_list[i+1])
    src1 = cv2.resize(img1, (640, 480))
    src2 = cv2.resize(img2, (640, 480))
 
    for it in range(WAIT+1):
        if it % 100 == 0:
            weight = it / WAIT
            res = cv2.addWeighted(src1, 1-weight, src2, weight, 0)
            cv2.imshow('images', res)
            cv2.waitKey(100)
 
cv2.waitKey(0)
cv2.destroyAllWindows()
```
