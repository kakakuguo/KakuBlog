---
title: AlexNet
description: AlexNet是一种深度卷积神经网络，AlexNet 被认为是计算机视觉领域最有影响力的论文之一，刺激了更多使用卷积神经网络和 GPU 来加速深度学习的研究。
pubDate: 07 27 2025
image: /image/AlexNet.png
draft: true
categories:
  - 深度学习
tags:
  - AlexNet
  - 卷积神经网络
  - pytorch
  - python
  - Kaku
---

# 深度卷积神经网络（AlexNet）

2012年，AlexNet横空出世。它首次证明了学习到的特征可以超越手工设计的特征。它一举打破了计算机视觉研究的现状。 AlexNet使用了8层卷积神经网络，并以很大的优势赢得了2012年ImageNet图像识别挑战赛。

AlexNet和LeNet的架构非常相似，如下图所示。 注意，这里提供的是一个稍微精简版本AlexNet，去除了当年需要两个小型GPU同时运算的设计特点。

![AlexNet和LeNet对比图](../../../public/image/AlexNet2.svg)

AlexNet和LeNet的设计理念非常相似，但也存在显著差异。

1. AlexNet比相对较小的LeNet5要深得多。AlexNet由八层组成：五个卷积层、两个全连接隐藏层和一个全连接输出层。

2. AlexNet使用ReLU而不是sigmoid作为其激活函数。

3. AlexNet的池化层采用最大汇聚层而不是平均汇聚层

4. AlexNet中采用了暂退法来防止过拟合

面的内容将深入研究AlexNet的细节。

## 模型设计

在AlexNet的第一层，卷积窗口的形状是。 由于ImageNet中大多数图像的宽和高比MNIST图像的多10倍以上，因此，需要一个更大的卷积窗口来捕获目标。 第二层中的卷积窗口形状被缩减为5 x 5，然后是3 x 3。 此外，在第一层、第二层和第五层卷积层之后，加入窗口形状为、步幅为2的最大汇聚层。 而且，AlexNet的卷积通道数目是LeNet的10倍。

在最后一个卷积层后有两个全连接层，分别有4096个输出。 这两个巨大的全连接层拥有将近1GB的模型参数。 由于早期GPU显存有限，原版的AlexNet采用了双数据流设计，使得每个GPU只负责存储和计算模型的一半参数。 幸运的是，现在GPU显存相对充裕，所以现在很少需要跨GPU分解模型。

## 激活函数

此外，AlexNet将sigmoid激活函数改为更简单的ReLU激活函数。 一方面，ReLU激活函数的计算更简单，它不需要如sigmoid激活函数那般复杂的求幂运算。 另一方面，当使用不同的参数初始化方法时，ReLU激活函数使训练模型更加容易。 当sigmoid激活函数的输出非常接近于0或1时，这些区域的梯度几乎为0，因此反向传播无法继续更新一些模型参数。 相反，ReLU激活函数在正区间的梯度总是1。 因此，如果模型参数没有正确初始化，sigmoid函数可能在正区间内得到几乎为0的梯度，从而使模型无法得到有效的训练。

## 容量控制和预处理

AlexNet通过暂退法控制全连接层的模型复杂度，而LeNet只使用了权重衰减。 为了进一步扩充数据，AlexNet在训练时增加了大量的图像增强数据，如翻转、裁切和变色。 这使得模型更健壮，更大的样本量有效地减少了过拟合。

```python
import torch
from torch import nn
from d2l import torch as d2l
net == nn.Sequential(
    # 这里使用一个11*11的更大窗口来捕捉对象。
    # 同时，步幅为4，以减少输出的高度和宽度。
    # 另外，输出通道的数目96远大于LeNet
    nn.Conv2d(1, 96, kernel_size=11, stride=4), nn.ReLU(),
    nn.MaxPool2d(kernel_size=3, stride=2)
    # 减小卷积窗口，使用填充为2来使得与上一层的高和宽一致，且增大输出通道数
    nn.Conv2d(96, 256, kernel_size=5, padding=2), nn.ReLU(),
    nn.MaxPool2d(kernel_size=3, stride=2)
    # 使用三个连续的卷积层和较小的卷积窗口。
    # 除了最后的卷积层，输出通道的数量进一步增加。
    nn.Conv2d(256, 384, kernel_size=3, padding=1), nn.ReLU(),
    nn.Conv2d(384, 384, kernel_size=3, padding=1), nn.ReLU(),
    nn.Conv2d(384, 256, kernel_size=3, padding=1), nn.ReLU(),
    nn.MaxPool2d(kernel_size=3, stride=2),
    # 将四维数据展开成两维
    nn.Flatten(),
    # 这里，全连接层的输出数量是LeNet中的好几倍。使用dropout层来减轻过拟合
    nn.Linear(6400, 4096), nn.ReLU(),
    nn.Dropout(p=0.5),
    nn.Linear(4096, 4096), nn.ReLU(),
    nn.Dropout(p=0.5),
    # 最后是输出层。由于硬件限制这里使用Fashion-MNIST数据集，所以用类别数为10，而不是1000
    nn.Linear(4096, 10)
)
```

尽管AlexNet是在ImageNet上进行训练的，但在这里使用的是Fashion-MNIST数据集。因为即使在现代GPU上，训练ImageNet模型，同时使其收敛可能需要数小时或数天的时间。 将AlexNet直接应用于Fashion-MNIST的一个问题是，Fashion-MNIST图像的分辨率低于ImageNet图像。 为了解决这个问题，我们将它们增加到（通常来讲这不是一个明智的做法，但在这里这样做是为了有效使用AlexNet架构）。 

```python
# 批量大小
batch_size = 128
#读取数据集并将图片拉伸到224 x 224
train_iter, test_iter = d2l.load_data_fashion_mnist(batch_size, resize=224)
```

现在AlexNet可以开始被训练了。与 :numref:`sec_lenet`中的LeNet相比，这里的主要变化是使用更小的学习速率训练，这是因为网络更深更广、图像分辨率更高，训练卷积神经网络就更昂贵。

```python
# 学习率和循环训练次数
lr, num_epochs = 0.01, 10
d2l.train_ch6(net, train_iter, test_iter, num_epochs, lr, d2l.try_gpu())
```

![训练结果](../../../public/image/AlexNet3.png)
