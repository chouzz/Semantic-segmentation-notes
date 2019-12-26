# DeepLab系列笔记

2019年了，Deeplab系列已经被研究的很深入了，这里可以结合原文直接搜索其他人的阅读笔记，快速阅读论文。


DeepLabv1：使用空洞卷积(atrous convolution)来明确控制在深度卷积神经网络中计算特征响应的分辨率。  

DeepLabv2：使用空间金字塔金字塔池（ASPP），通过具有多种采样率和有效视场的滤镜，以多种尺度稳健地分割对象。   

DeepLabv3：通过图像级功能扩展了ASPP模块，以捕获更长距离的信息。我们还包括批归一化参数，以方便训练。特别是，我们在训练和评估过程中应用空洞卷积来提取不同输出步幅的输出特征，从而有效地在输出步幅=16时训练BN，并在评估过程中在输出步幅=8时获得高性能。

DeepLabv3+：将DeepLabv3扩展为包括一个简单而有效的解码器模块，以优化分割结果，尤其是沿对象边界的分割结果。此外，在这种编码器-解码器结构中，可以通过空洞卷积来任意权衡提取的编码器特征的分辨率，以权衡精度和运行时间。

## DeeplabV1:Semantic Image Segmentation with Deep Convolutional Nets and Fully Connected CRFs

https://zhuanlan.zhihu.com/p/37124598
https://zhuanlan.zhihu.com/p/68531147


## DeeplabV2:

s
## DeeplabV3:


## DeeplabV3+:




# 参考链接

https://github.com/tensorflow/models/tree/master/research/deeplab


使 ResNet 在保持参数量不变、每个阶段的卷积层视野不变的前提下，靠后的卷积层也可保持较大的 feature maps 尺寸从而有利于对小目标的检测，提高模型整体性能