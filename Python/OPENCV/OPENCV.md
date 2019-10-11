#
### [去除符水印](https://www.cnblogs.com/dockers/p/9902202.html)
```
#!/usr/bin/env python
# -*- coding:utf-8 -*-
 
# Author : zhibo.wang
# E-mail : d_1206@qq.com
# Date   : 18/11/03 20:07:41
# Desc   :
 
 
import cv2
import numpy as np
 
 
def img_clean(img):
    height, width = img.shape[0:2]
 
    cv2.namedWindow("Image", 0)
    cv2.resizeWindow("Image", int(width / 2), int(height / 2))
    cv2.imshow('Image', img)
 
    rects = ((width - 170, height - 38, width, height),(1, 1, 164, 100)) #水印区域
    mask = np.zeros((height, width), np.uint8)
    for rect in rects:
        x1, y1, x2, y2 = rect
        cv2.rectangle(mask, (x1, y1), (x2, y2), (255, 255, 255), -1)
        img = cv2.inpaint(img, mask, 1.5, cv2.INPAINT_TELEA) #蒙版
 
    cv2.namedWindow("newImage", 0)
    cv2.resizeWindow("newImage", int(width / 2), int(height / 2))
    cv2.imshow('newImage', img)
    cv2.waitKey(0)
    cv2.destroyAllWindows()
 
 
if __name__ == '__main__':
    f_img = 'shui1.jpg'
    img = cv2.imread(f_img)
    img_clean(img)
```

### 更改顏色空間
```
學習目標

1、學習如何將圖像從一個色彩空間轉換為另一個色彩空間，如BGR --- Gray，BGR --- HSV等；
2、我們還將創建一個應用程式，用於在視頻中提取彩色物件；
3、學習以下功能：cv2.cvtColor（），cv2.inRange（）等。

1、改變顏色空間

OpenCV中有150多種顏色空間轉換方法。 但目前只研究使用最廣泛的兩種，BGR --- Gray和BGR --- HSV。

使用函數：cv2.cvtColor(input_image, flag)，flag：確定轉換的類型。

BGR---Gray：使用的flag對應的是：cv2.COLOR_BGR2GRAY；

（注意：OpenCV裡面是B、G、R這樣的方式，千萬要區別於R、G、B。）

BGR---HSV：使用的flag對應的是：cv2.COLOR_BGR2HSV；

範例（觀察顏色轉換的方法有）：

#coding:utf8
import cv2
 
flags = [i for i in dir(cv2) if i.startswith('COLOR_')]
print (flags)


這三行代碼是為了讓我們查看其餘的以“COLOR_”開頭的全部命令。注意：在第2句程式中的這種正則化的程式設計方式是需要借鑒並且學會使用的。

輸出：

['COLOR_BAYER_BG2BGR', 'COLOR_BAYER_BG2BGRA', 'COLOR_BAYER_BG2BGR_EA', 'COLOR_BAYER_BG2BGR_VNG', 'COLOR_BAYER_BG2GRAY', 'COLOR_BAYER_BG2RGB', 'COLOR_BAYER_BG2RGBA', 'COLOR_BAYER_BG2RGB_EA', 'COLOR_BAYER_BG2RGB_VNG', 'COLOR_BAYER_GB2BGR', 'COLOR_BAYER_GB2BGRA', 'COLOR_BAYER_GB2BGR_EA', 'COLOR_BAYER_GB2BGR_VNG', 'COLOR_BAYER_GB2GRAY', 'COLOR_BAYER_GB2RGB', 'COLOR_BAYER_GB2RGBA', 'COLOR_BAYER_GB2RGB_EA', 'COLOR_BAYER_GB2RGB_VNG', 'COLOR_BAYER_GR2BGR', 'COLOR_BAYER_GR2BGRA', 'COLOR_BAYER_GR2BGR_EA', 'COLOR_BAYER_GR2BGR_VNG', 'COLOR_BAYER_GR2GRAY', 'COLOR_BAYER_GR2RGB', 'COLOR_BAYER_GR2RGBA', 'COLOR_BAYER_GR2RGB_EA', 'COLOR_BAYER_GR2RGB_VNG', 'COLOR_BAYER_RG2BGR', 'COLOR_BAYER_RG2BGRA', 'COLOR_BAYER_RG2BGR_EA', 'COLOR_BAYER_RG2BGR_VNG', 'COLOR_BAYER_RG2GRAY', 'COLOR_BAYER_RG2RGB', 'COLOR_BAYER_RG2RGBA', 'COLOR_BAYER_RG2RGB_EA', 'COLOR_BAYER_RG2RGB_VNG', 'COLOR_BGR2BGR555', 'COLOR_BGR2BGR565', 'COLOR_BGR2BGRA', 'COLOR_BGR2GRAY', 'COLOR_BGR2HLS', 'COLOR_BGR2HLS_FULL', 'COLOR_BGR2HSV', 'COLOR_BGR2HSV_FULL', 'COLOR_BGR2LAB', 'COLOR_BGR2LUV', 'COLOR_BGR2Lab', 'COLOR_BGR2Luv', 'COLOR_BGR2RGB', 'COLOR_BGR2RGBA', 'COLOR_BGR2XYZ', 'COLOR_BGR2YCR_CB', 'COLOR_BGR2YCrCb', 'COLOR_BGR2YUV', 'COLOR_BGR2YUV_I420', 'COLOR_BGR2YUV_IYUV', 'COLOR_BGR2YUV_YV12', 'COLOR_BGR5552BGR', 'COLOR_BGR5552BGRA', 'COLOR_BGR5552GRAY', 'COLOR_BGR5552RGB', 'COLOR_BGR5552RGBA', 'COLOR_BGR5652BGR', 'COLOR_BGR5652BGRA', 'COLOR_BGR5652GRAY', 'COLOR_BGR5652RGB', 'COLOR_BGR5652RGBA', 'COLOR_BGRA2BGR', 'COLOR_BGRA2BGR555', 'COLOR_BGRA2BGR565', 'COLOR_BGRA2GRAY', 'COLOR_BGRA2RGB', 'COLOR_BGRA2RGBA', 'COLOR_BGRA2YUV_I420', 'COLOR_BGRA2YUV_IYUV', 'COLOR_BGRA2YUV_YV12', 'COLOR_BayerBG2BGR', 'COLOR_BayerBG2BGRA', 'COLOR_BayerBG2BGR_EA', 'COLOR_BayerBG2BGR_VNG', 'COLOR_BayerBG2GRAY', 'COLOR_BayerBG2RGB', 'COLOR_BayerBG2RGBA', 'COLOR_BayerBG2RGB_EA', 'COLOR_BayerBG2RGB_VNG', 'COLOR_BayerGB2BGR', 'COLOR_BayerGB2BGRA', 'COLOR_BayerGB2BGR_EA', 'COLOR_BayerGB2BGR_VNG', 'COLOR_BayerGB2GRAY', 'COLOR_BayerGB2RGB', 'COLOR_BayerGB2RGBA', 'COLOR_BayerGB2RGB_EA', 'COLOR_BayerGB2RGB_VNG', 'COLOR_BayerGR2BGR', 'COLOR_BayerGR2BGRA', 'COLOR_BayerGR2BGR_EA', 'COLOR_BayerGR2BGR_VNG', 'COLOR_BayerGR2GRAY', 'COLOR_BayerGR2RGB', 'COLOR_BayerGR2RGBA', 'COLOR_BayerGR2RGB_EA', 'COLOR_BayerGR2RGB_VNG', 'COLOR_BayerRG2BGR', 'COLOR_BayerRG2BGRA', 'COLOR_BayerRG2BGR_EA', 'COLOR_BayerRG2BGR_VNG', 'COLOR_BayerRG2GRAY', 'COLOR_BayerRG2RGB', 'COLOR_BayerRG2RGBA', 'COLOR_BayerRG2RGB_EA', 'COLOR_BayerRG2RGB_VNG', 'COLOR_COLORCVT_MAX', 'COLOR_GRAY2BGR', 'COLOR_GRAY2BGR555', 'COLOR_GRAY2BGR565', 'COLOR_GRAY2BGRA', 'COLOR_GRAY2RGB', 'COLOR_GRAY2RGBA', 'COLOR_HLS2BGR', 'COLOR_HLS2BGR_FULL', 'COLOR_HLS2RGB', 'COLOR_HLS2RGB_FULL', 'COLOR_HSV2BGR', 'COLOR_HSV2BGR_FULL', 'COLOR_HSV2RGB', 'COLOR_HSV2RGB_FULL', 'COLOR_LAB2BGR', 'COLOR_LAB2LBGR', 'COLOR_LAB2LRGB', 'COLOR_LAB2RGB', 'COLOR_LBGR2LAB', 'COLOR_LBGR2LUV', 'COLOR_LBGR2Lab', 'COLOR_LBGR2Luv', 'COLOR_LRGB2LAB', 'COLOR_LRGB2LUV', 'COLOR_LRGB2Lab', 'COLOR_LRGB2Luv', 'COLOR_LUV2BGR', 'COLOR_LUV2LBGR', 'COLOR_LUV2LRGB', 'COLOR_LUV2RGB', 'COLOR_Lab2BGR', 'COLOR_Lab2LBGR', 'COLOR_Lab2LRGB', 'COLOR_Lab2RGB', 'COLOR_Luv2BGR', 'COLOR_Luv2LBGR', 'COLOR_Luv2LRGB', 'COLOR_Luv2RGB', 'COLOR_M_RGBA2RGBA', 'COLOR_RGB2BGR', 'COLOR_RGB2BGR555', 'COLOR_RGB2BGR565', 'COLOR_RGB2BGRA', 'COLOR_RGB2GRAY', 'COLOR_RGB2HLS', 'COLOR_RGB2HLS_FULL', 'COLOR_RGB2HSV', 'COLOR_RGB2HSV_FULL', 'COLOR_RGB2LAB', 'COLOR_RGB2LUV', 'COLOR_RGB2Lab', 'COLOR_RGB2Luv', 'COLOR_RGB2RGBA', 'COLOR_RGB2XYZ', 'COLOR_RGB2YCR_CB', 'COLOR_RGB2YCrCb', 'COLOR_RGB2YUV', 'COLOR_RGB2YUV_I420', 'COLOR_RGB2YUV_IYUV', 'COLOR_RGB2YUV_YV12', 'COLOR_RGBA2BGR', 'COLOR_RGBA2BGR555', 'COLOR_RGBA2BGR565', 'COLOR_RGBA2BGRA', 'COLOR_RGBA2GRAY', 'COLOR_RGBA2M_RGBA', 'COLOR_RGBA2RGB', 'COLOR_RGBA2YUV_I420', 'COLOR_RGBA2YUV_IYUV', 'COLOR_RGBA2YUV_YV12', 'COLOR_RGBA2mRGBA', 'COLOR_XYZ2BGR', 'COLOR_XYZ2RGB', 'COLOR_YCR_CB2BGR', 'COLOR_YCR_CB2RGB', 'COLOR_YCrCb2BGR', 'COLOR_YCrCb2RGB', 'COLOR_YUV2BGR', 'COLOR_YUV2BGRA_I420', 'COLOR_YUV2BGRA_IYUV', 'COLOR_YUV2BGRA_NV12', 'COLOR_YUV2BGRA_NV21', 'COLOR_YUV2BGRA_UYNV', 'COLOR_YUV2BGRA_UYVY', 'COLOR_YUV2BGRA_Y422', 'COLOR_YUV2BGRA_YUNV', 'COLOR_YUV2BGRA_YUY2', 'COLOR_YUV2BGRA_YUYV', 'COLOR_YUV2BGRA_YV12', 'COLOR_YUV2BGRA_YVYU', 'COLOR_YUV2BGR_I420', 'COLOR_YUV2BGR_IYUV', 'COLOR_YUV2BGR_NV12', 'COLOR_YUV2BGR_NV21', 'COLOR_YUV2BGR_UYNV', 'COLOR_YUV2BGR_UYVY', 'COLOR_YUV2BGR_Y422', 'COLOR_YUV2BGR_YUNV', 'COLOR_YUV2BGR_YUY2', 'COLOR_YUV2BGR_YUYV', 'COLOR_YUV2BGR_YV12', 'COLOR_YUV2BGR_YVYU', 'COLOR_YUV2GRAY_420', 'COLOR_YUV2GRAY_I420', 'COLOR_YUV2GRAY_IYUV', 'COLOR_YUV2GRAY_NV12', 'COLOR_YUV2GRAY_NV21', 'COLOR_YUV2GRAY_UYNV', 'COLOR_YUV2GRAY_UYVY', 'COLOR_YUV2GRAY_Y422', 'COLOR_YUV2GRAY_YUNV', 'COLOR_YUV2GRAY_YUY2', 'COLOR_YUV2GRAY_YUYV', 'COLOR_YUV2GRAY_YV12', 'COLOR_YUV2GRAY_YVYU', 'COLOR_YUV2RGB', 'COLOR_YUV2RGBA_I420', 'COLOR_YUV2RGBA_IYUV', 'COLOR_YUV2RGBA_NV12', 'COLOR_YUV2RGBA_NV21', 'COLOR_YUV2RGBA_UYNV', 'COLOR_YUV2RGBA_UYVY', 'COLOR_YUV2RGBA_Y422', 'COLOR_YUV2RGBA_YUNV', 'COLOR_YUV2RGBA_YUY2', 'COLOR_YUV2RGBA_YUYV', 'COLOR_YUV2RGBA_YV12', 'COLOR_YUV2RGBA_YVYU', 'COLOR_YUV2RGB_I420', 'COLOR_YUV2RGB_IYUV', 'COLOR_YUV2RGB_NV12', 'COLOR_YUV2RGB_NV21', 'COLOR_YUV2RGB_UYNV', 'COLOR_YUV2RGB_UYVY', 'COLOR_YUV2RGB_Y422', 'COLOR_YUV2RGB_YUNV', 'COLOR_YUV2RGB_YUY2', 'COLOR_YUV2RGB_YUYV', 'COLOR_YUV2RGB_YV12', 'COLOR_YUV2RGB_YVYU', 'COLOR_YUV420P2BGR', 'COLOR_YUV420P2BGRA', 'COLOR_YUV420P2GRAY', 'COLOR_YUV420P2RGB', 'COLOR_YUV420P2RGBA', 'COLOR_YUV420SP2BGR', 'COLOR_YUV420SP2BGRA', 'COLOR_YUV420SP2GRAY', 'COLOR_YUV420SP2RGB', 'COLOR_YUV420SP2RGBA', 'COLOR_YUV420p2BGR', 'COLOR_YUV420p2BGRA', 'COLOR_YUV420p2GRAY', 'COLOR_YUV420p2RGB', 'COLOR_YUV420p2RGBA', 'COLOR_YUV420sp2BGR', 'COLOR_YUV420sp2BGRA', 'COLOR_YUV420sp2GRAY', 'COLOR_YUV420sp2RGB', 'COLOR_YUV420sp2RGBA', 'COLOR_mRGBA2RGBA']
注意：

對於HSV，色調範圍為[0,179]，飽和度範圍為[0,255]，值範圍為[0,255]。 不同的軟體使用不同的比例。 因此，如果您正在比較OpenCV值與他們，您需要規範化這些範圍。

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
