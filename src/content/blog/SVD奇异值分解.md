---
title: SVD奇异值分解
description: SVD是最广泛使用的无监督学习算法之一，它在许多推荐系统和降维系统中都居于核心位置。
pubDate: 07 29 2025
draft: false
categories:
- 数学
tags:
- SVD
- 奇异值分解
- 线性代数
- Kaku
---

## 介绍

线性代数是机器学习领域的基础，其中一个最重要的概念是奇异值分解（SVD），本文尽可能简洁的介绍SVD（奇异值分解）算法的基础理解，以及它在现实世界中的应用。

SVD是最广泛使用的无监督学习算法之一，它在许多推荐系统和降维系统中居于核心位置，这些系统是全球公司如谷歌、Netflix、Facebook、YouTube等的核心技术。

简单来说，SVD是将一个任意矩阵分解为三个矩阵。所以如果我们有一个矩阵A，那么它的SVD可以表示为：$A_{m×n}=U_{m×m}S_{m×n}V^T_{n×n}$。

> 其中A时要分解的矩阵,U和V都是正交矩阵,S是非负对角阵。

用矩阵的形式表示为:

$$
\underset{m \times m}{\begin{pmatrix} 
x_{11} & x_{12} & \cdots & x_{1n} \\ 
\vdots & \vdots & \ddots & \vdots \\ 
x_{m1} & m \times n & x_{mn} & \cdots \\ 
\end{pmatrix}} 
= 
\underset{m \times m}{\begin{pmatrix} 
u_{11} & u_{m1} \\ 
\vdots & \vdots \\ 
u_{1m} & u_{mm} \\ 
\end{pmatrix}}
\underset{m \times n}{\begin{pmatrix} 
\sigma_1 & 0 \\ 
\vdots & \sigma_r \\ 
0 & 0 \\ 
 \end{pmatrix}}
\underset{n \times n}{\begin{pmatrix} 
v_{11} & v_{1n} \\ 
\vdots & \vdots \\ 
v_{n1} & v_{nn} \\ 
\end{pmatrix}}
$$

> PS: 我们通常将具有较大特征值的向量排列在前，而较小特征值的向量则排在后面。

与特征值分解相比，奇异值分解可以应用于非方阵。在SVD中，U和 V 对于任何矩阵都是可逆的，并且它们是正交归一的，这是我们所喜爱的特性。

## 示例

$$
A=\begin{pmatrix}
3 & 2 & 3 \\
2 & 3 & -2 
\end{pmatrix}
$$

我们分别计算矩阵与其转置的乘积和其转置与矩阵的成绩:

$$
AA^T=\begin{pmatrix}
17 & 8 \\
8 & 17  
\end{pmatrix} 
\quad
A^TA=\begin{pmatrix}
13 & 12 & 2 \\
13 & 13  & -2 \\
2 & -2  & 8
\end{pmatrix}
$$

然后求解$AA^T$的特征值和特征向量:

特征值：$ \lambda_1 = 25，\lambda_2 = 9$
对应的特征向量：

$$
u_1 = \begin{pmatrix} 
1/\sqrt{2} \\ 
1/\sqrt{2} 
\end{pmatrix}
\quad
u_2 = \begin{pmatrix} 
1/\sqrt{2} \\ 
-1/\sqrt{2} 
\end{pmatrix}\\ 
$$

即矩阵U表示为：

$$
U = (u_1, u_2) = \begin{pmatrix} 
1/\sqrt{2} & 1/\sqrt{2} \\ 
1/\sqrt{2} & -1/\sqrt{2} 
\end{pmatrix}
$$

同理求解$A^TA$的特征值和特征向量:

特征值： \lambda_1 = 25，\lambda_2 = 9$
对应的特征向量：

$$
v_1 = \begin{pmatrix} 
1/\sqrt{2} \\ 
1/\sqrt{2} \\
0
\end{pmatrix}
\quad
v_2 = \begin{pmatrix} 
1/\sqrt{18} \\ 
-1/\sqrt{18} \\
4/\sqrt{18} 
\end{pmatrix}
\quad
v_3 = \begin{pmatrix} 
2/3 \\ 
-2/3 \\
-1/3 
\end{pmatrix}\\ 
$$

即矩阵V表示为：

$$
V = (v_1, v_2, v_3) = \begin{pmatrix} 
1/\sqrt{2} & 1/\sqrt{18}  & 2/3\\ 
1/\sqrt{2} & -1/\sqrt{18}  & -2/3\\ 
0 & 4/\sqrt{18}  & -1/3\\ 
\end{pmatrix}
$$

奇异值是正特征值的平方根，即5和3。因此矩阵A的SVD分解为：

$$
A=USV^T=
\begin{pmatrix} 
1/\sqrt{2} & 1/\sqrt{2} \\ 
1/\sqrt{2} & -1/\sqrt{2} 
\end{pmatrix}

\begin{pmatrix}
5 & 0 & 0 \\
0 & 3 & 0 \\
\end{pmatrix}

\begin{pmatrix} 
1/\sqrt{2} & 1/\sqrt{2}  & 0\\ 
1/\sqrt{18} & -1/\sqrt{18}  & 4/\sqrt{18}\\ 
2/3 & -2/3  & -1/3\\ 
\end{pmatrix}
$$

## SVD分解证明

为了得到矩阵A的SVD分解，我们要求出$A=USV^T$中的U,S,V。

因为U,V都为正交矩阵，所以可得：$U^TU=I,V^TV=I$,其中I为单位矩阵。$A^T=(USV^T)^T=VS^TU^T=VSU^T$,由此可得$A^TA=VSU^TUSV^T=VS^2V^T=VS^2V^{-1}$。

又因为$(A^TA)^T=A^TA$,所以$A^TA$为对称矩阵,因此可以直接按特征值和特征向量进行SVD分解,分解后为$VS^2V^{-1}$,由此可知V为$A^TA$的特征向量组成的矩阵,$S$为$A^TA$的特征值组成的对角矩阵的平方根。

同理可得U为$AA^T$的特征向量组成的矩阵,$S$为$AA^T$的特征值组成的对角矩阵的平方根。

因此只要求出$AA^T$和$A^TA$对应的所有特征向量和特征值即可求出A的奇异向量和奇异值

> PS: 当矩阵A的行空间和列空间为1时,我们可以直接算出非零奇异值对应的行空间奇异向量$v_1$和列奇异向量$u_1$。
