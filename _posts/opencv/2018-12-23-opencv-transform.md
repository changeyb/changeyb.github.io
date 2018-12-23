---
layout: post
title:  "opencv中的几何变换"
categories: opencv
tags:  opencv 仿射变换 透射变换 二维变换 三维变换 warpPerspective warpAffine
author: Benjamin
---

* content
{:toc}

图像的几何变换主要可以分为2种：仿射变换和透视变换。

仿射变换是一种线性变换，也称二维变换。图像上的两条线变换前是平行线，变换后还是平行线。

投射变换是一种非线性变换，也称三维变换。变换后的图像不能维持以前平行线的关系。





## 1. 仿射变换和透视变换原理

### 1.1 仿射变换

仿射变换的变换矩阵 $M$ 是一个2行3列的矩阵。假设原图像素点坐标为 $(u, v)$ ,变换后的点为 $(x, y)$，则有：

$$
  \begin{bmatrix}
    x \\
    y
  \end{bmatrix}
  =
  M
  \begin{bmatrix}
    u \\
    v \\
    1
  \end{bmatrix}
  =
  \begin{bmatrix}
    a_{11} & a_{12} & a_{13} \\
    a_{21} & a_{22} & a_{23}
  \end{bmatrix}
  \begin{bmatrix}
    u \\
    v \\
    1
  \end{bmatrix} \tag{1.1}
$$

由 $(1)$ 可推出：
$$
\begin{align}
x  = a_{11}u + a_{12}v + a_{13} \\
y  = a_{21}u + a_{22}v + a_{23}
\end{align}
\tag{1.2}
$$
实际图像仿射变换处理过程：是先获得变换矩阵 $M$，再根据 $M$ 和原图像像素点坐标根据公式 $(1.1)$ 求得新图像的像素点坐标。而根据公式 $(1.2)$，要想得到 $M$，需要解6个未知数，所以至少需要知道**仿射变换前的3个点的座标和仿射变换后的3个点坐标**，组成6个方程。

### 1.2 透视变换

透射变换的变换矩阵 $M$ 是一个3行3列的矩阵。假设原图像素点坐标为 $(u, v)$ ,变换后的点为 $(x, y)$，则有：

$$
  \begin{bmatrix}
    x_{t} \\
    y_{t} \\
    z_{t}
  \end{bmatrix}
  =
  M
  \begin{bmatrix}
    u \\
    v \\
    1
  \end{bmatrix}
  =
  \begin{bmatrix}
    a_{11} & a_{12} & a_{13} \\
    a_{21} & a_{22} & a_{23} \\
    a_{31} & a_{32} & a_{33}
  \end{bmatrix}
  \begin{bmatrix}
    u \\
    v \\
    1
  \end{bmatrix} \tag{2.1}
$$

由 $(2.1)$ 可推出：
$$
\begin{align}
x_t = a_{11}u + a_{12}v + a_{13} \\
y_t = a_{21}u + a_{22}v + a_{23} \\
z_t = a_{31}u + a_{32}v + a_{33}
\end{align}
\tag{2.2}
$$
新像素点 $x, y$ 的值分别为：
$$
\begin{align}
x = \frac{x_t}{z_t}=\frac{a_{11}u + a_{12}v + a_{13}}{a_{31}u + a_{32}v + a_{33}}=\frac{k_{11}u + k_{12}v + k_{13}}{k_{31}u + k_{32}v + 1} \\
y = \frac{y_t}{x_t}=\frac{a_{21}u + a_{22}v + a_{23}}{a_{31}u + a_{32}v + a_{33}}=\frac{k_{21}u + k_{22}v + k_{23}}{k_{31}u + k_{32}v + 1}
\end{align}
\tag{2.3}
$$
实际图像透视变换处理过程：是先获得变换矩阵 $M$，再根据原图像像素点坐标和公式 $(2.3)$ 求得新图像的像素点坐标。而根据公式 $(2.3)$，要想得到 $M$，需要解8个未知数，所以至少需要知道**透视变换前的4个点的坐标和仿射变换后的4个点坐标**，组成8个方程。

## 2. opencv仿射变换和透视变换

根据前面提到的图像处理过程，进行仿射变换前，需要获取仿射变换矩阵；进行透视变换前需要获取图形的透视变换矩阵。

### 2.1 仿射变换
示例代码：
```
import cv2
import numpy as np
from matplotlib import pyplot as plt

image = cv2.imread('test.jpg')
#原图像3个点坐标和变换后图像的3个点坐标
old_axis = np.float32([[0, 0], [100, 0], [0, 100]])
new_axis = np.float32([[50, 50], [150, 50], [50, 150]])

# 获取仿射变换矩阵
M = cv2.getAffineTransform(old_axis, new_axis)
# 进行仿射变换，变换后的图像与原图像大小保持一致
image = cv2.warpAffine(image, M, image.shape[:2])

# 显示图像
plt.imshow(image[:,:,(2,1,0)])
plt.xticks([]), plt.yticks([])
plt.show()
```

### 2.2 透视变换
示例代码：
```
import cv2
import numpy as np
from matplotlib import pyplot as plt

image = cv2.imread('test.jpg')
#原图像3个点坐标和变换后图像的3个点坐标
old_axis = np.float32([[0, 0], [590, 0], [0, 590], [590, 590]])
new_axis = np.float32([[50, 50], [590, 0], [0, 590], [400, 400]])

# 获取仿射变换矩阵
M = cv2.getPerspectiveTransform(old_axis, new_axis)
# 进行仿射变换，变换后的图像与原图像大小保持一致
image = cv2.warpPerspective(image, M, image.shape[:2])

# 显示图像
plt.imshow(image[:,:,(2,1,0)])
plt.xticks([]), plt.yticks([])
plt.show()
```
