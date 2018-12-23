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





## 仿射变换和透视变换原理

### 仿射变换

仿射变换的变换矩阵M是一个2行3列的矩阵。假设原图像素点坐标为 $(u, v)$ ,变换后的点为 $(x, y)$，则有：

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
  \end{bmatrix} \tag{1}
$$

由 $(1)$ 可推出：
$$
\begin{align}
x  = a_{11}u + a_{12}v + a_{13} \\
y  = a_{21}u + a_{22}v + a_{23}
\end{align}
\tag{2}
$$
