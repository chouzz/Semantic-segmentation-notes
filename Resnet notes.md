- [ResNet(Deep Residual Learning for Image Recognition)](#resnetdeep-residual-learning-for-image-recognition)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [问题的提出](#%e9%97%ae%e9%a2%98%e7%9a%84%e6%8f%90%e5%87%ba)
  - [网络结构](#%e7%bd%91%e7%bb%9c%e7%bb%93%e6%9e%84)
  - [实施细节](#%e5%ae%9e%e6%96%bd%e7%bb%86%e8%8a%82)

# ResNet(Deep Residual Learning for Image Recognition)

## 概述

2015 年，由微软亚洲研究院何凯明等人发表的 ResNet 网络，成功的将网络层数加到更深的层次，并且获得了很好的效果，其复杂度也与之前的 vgg 网络相差不大，并且获得到了 ILSVRC 2015 和 COCO 2015 的分类任务竞赛冠军，同样也在 CIFAR-10 数据集上进行了 100 到 1000 层的测试。

## 问题的提出

<center>
<img src=./image/深层网络误差更大的现象.png alt="深层网络误差更大的现象"  width="60%" height="60%" />

Fig.1 深层网络误差更大的现象

</center>

是否越深的网络学习的就会更好？如上图所示，作者在 CIFAR-10 数据集上进行实验，发现 56 层的网络无论是在训练误差还是在测试误差上效果都比 20 层网络的效果差，这说明并不是越深的网络效果就会越好，因为深层网络带来梯度消失或者爆炸问题，导致深层网络的误差加大，一些现在已有的常用的方法是使用正则化初始化和中间初始化来解决，而当随着网络层数的加深，精度达到饱和的时候，继续进行训练精度反而快速下降，这种现象并不是因为过拟合导致的，论文给出猜想，添加一层额外的恒等映射，如下图所示：

<center>
<img src=./image/残差学习模块.png alt="ResNet提出的剩余/残差学习模块"  width="60%" height="60%" />

Fig.2 ResNet 提出的剩余/残差学习模块

</center>

这就是论文一开始提出 ResNet 模块，论文中提到了还有很多和短连接相关的工作，这里的短连接就是恒等映射，然后将输出加上叠层网络，最后输出的就是$F(x)+x$了。  
然后提出了 ResNet 有 2 个优点：

1. 容易优化，其他建档叠加网络层数有很大的训练误差，也就是下图中所表现的 20 层和 56 层的训练误差
2. 比之前的网络如 vgg 能够获得更高的精度

作者使用该网络效果比 vgg 好，在 ImageNet 中误差率低，并在 ILSVRC2015 和 ImageNet 检测，定位和 COCO 分割竞赛中都获得了第一名，说明该网路确实是有很好的效果的。

---

## 网络结构

论文中提出了 2 种网络结构，一种是 plain 也就是原始的网络，另外一种是加上剩余学习或者叫做残差模块的残差网络，他们的网络结构如下表：

<center>
<img src=./image/vgg_plain_resnet.png alt="vgg19，plain34和ResNet34网络结构"  width="60%" height="60%" />

Fig.3 vgg19，plain34和ResNet34网络结构

</center>

从左到右依次是 vgg19，plain，和 resnet，每种网络都包含了 4 个模块，经过每个模块的池化之后，分别缩小到原图的 1/2, 1/4, 1/8, 1/16 大小,每个模块都包含不同数量的卷积层数，而 34 层的 ResNet 特殊的一点就是加入了短连接，也就是图中曲线部分。

plain 网络的想法来自于 vggnet，卷积层大多使用 3x3 的滤波器，然后遵循两条规则：

1. 对输出相同的特征图大小，网络有相同数量的滤波器
2. 如果特征图大小减半，滤波器数量加倍来保留每层网络的时间复杂度(这样为何可以保留时间复杂度？？)

## 实施细节

在 ImageNet 上的实现细节是跟着 vgg 论文来的。

- 数据增强： random crop 224x224, horizontal flip,per-pixel mean subtracted，标准色彩增强(standard color augmentation)
- 在卷积层激活函数层之间添加 BatchNormalization
- 初始化权重(来自于：Delving deep into rectifers: Surpassing human-level performance on imagenet classifcation)
- 优化器: SGD
- mini-batch: 256
- learning rate: 从 0.1 开始当误差停止时减小 10 倍
- 迭代次数：600K, 迭代次数太多啦。。。
- weight decay: 0.0001
- momentum: 0.9
- 没有用到 dropout

下图中左侧为 18 层和 34 层的 plain 网络的训练和验证误差，这里就有了退化问题，即 34 层的网络比 18 层网络的误差率更高，作者明确说明这种优化困难不是梯度消失造成的，因为 plain 网络已经使用 BN 进行了训练，确保了网络前向传播信号具有非 0 的方差，作者推测这是因为网络收敛速度极低，影响到了训练误差。
而下图中右侧为 18 层和 34 层的 ResNet 的训练和验证误差，作者提到从该图中可以观测到 3 点：

1. 残差学习可以扭转这种局面，34 层网络比 18 层网络误差更小，比 plain 网络有明显的区别，而且 34 层 ResNet 在验证数据上更好，表明 ResNet 可以很好的解决退化问题。
2. 和 plain 的 34 层网络相比，ResNet34 获得了更小的训练误差，表明了残差系统可以在极深的系统中学习
3. 和 palin 的 18 层网络相比，ResNet18 学习的更好，这说明了当网络没有那么深的时候(这里是 18 层),当前的 SGD 优化器仍然可以找到很好的解决方案，在这种情况下，ResNet 通过更快的收敛来简化优化。

<center>
<img src='./image/Plain and ResNet training on ImageNet.png'
 alt="Plain和ResNet网络在ImageNet上的训练和验证误差"  width="80%" height="80%" />

Fig.4 Plain 和 ResNet 网络在 ImageNet 上的训练和验证误差

</center>

ImageNet 中的结果，误差率如下图：

<center>
<img src='./image/imageNet error rate.png'
 alt="plain和ResNet在ImageNet中的误差率"  width="60%" height="60%" />

Fig.5 plain 和 ResNet 在 ImageNet 中的误差率

</center>

到此为止已经说明了 ResNet 的优势所在了，作者又提出了另一种 ResNet 模块，Bottleneck ResNet，和之前的 buildingResNet 一样，只不过多增加了一层卷积层，该模块用于 ResNet-50/101/152,如下图所示：

<center>
<img src='./image/Building ResNet and Bottleneck ResNet.png'
 alt="Building ResNet和Bottleneck ResNet"  width="60%" height="60%" />

Fig.6 Building ResNet 和 Bottleneck ResNet

</center>

其中的 ResNet101 和 ResNet152 具体网络结构如下图所示：

<center>
<img src='./image/Architectures for ImageNet.png'
 alt="ResNet在ImageNet上的具体网络架构"  width="60%" height="60%" />

Fig.7 ResNet 在 ImageNet 上的具体网络架构

</center>
