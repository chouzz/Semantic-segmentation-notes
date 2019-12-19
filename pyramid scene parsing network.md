- [Pyramid Scene Parsing Network(PSPnet)笔记](#pyramid-scene-parsing-networkpspnet%e7%ac%94%e8%ae%b0)
- [介绍](#%e4%bb%8b%e7%bb%8d)
- [现阶段问题](#%e7%8e%b0%e9%98%b6%e6%ae%b5%e9%97%ae%e9%a2%98)
- [金字塔池化模块](#%e9%87%91%e5%ad%97%e5%a1%94%e6%b1%a0%e5%8c%96%e6%a8%a1%e5%9d%97)
- [基于ResNet的FCN结构深度监督](#%e5%9f%ba%e4%ba%8eresnet%e7%9a%84fcn%e7%bb%93%e6%9e%84%e6%b7%b1%e5%ba%a6%e7%9b%91%e7%9d%a3)
- [实现细节](#%e5%ae%9e%e7%8e%b0%e7%bb%86%e8%8a%82)
- [结果](#%e7%bb%93%e6%9e%9c)
# Pyramid Scene Parsing Network(PSPnet)笔记

# 介绍
由香港大学在2017年发表的论文，主要提出了空间金字塔池化模块，能够更好的理解全局语义信息，利用PSPnet，作者在PASCAL VOC2012数据集上得到mIoU为85.4%，在Cityscapes数据集中得到80.2%的mIoU

# 现阶段问题
- 混淆类别。VOC2012仅有20个类别，当遇到类别较多时，如ADE20K数据集，多达100种thing和50个stuff类别，即使是标注数据的人也会混淆类别
- 不匹配的关系。例如水中的船被误识别为车，众所周知，水中是不可能存在车辆的，所以没有利用到物体和当前的场景信息。
- 不显眼的种类。例如小物体，被包括在大物体中的小类别等等，由于感受野的原因容易被忽视


# 金字塔池化模块

<center>
<img src='./image/PSP network architecture.png'  alt="PSPnet 架构"  width="100%" height="100%" />    

PSPnet 架构
</center>

如上图所示，该图为PSPnet的整体结构，其基于FCN和空洞卷积，并且使用了包含空洞卷积的ResNet预训练权重。其中图(c)即为空间金字塔池化模块，空间金字塔模块来源于金字塔匹配算法，用于在不同分辨率上统计图像特征点分布，获取图像的局部信息。该模块主要分为4个部分，最上方红色为全局池化后的单个输出，其下方的level将特征图分成不同子区域和形式，代表了不同的位置，每个level包含不同大小的特征图，后面接了1x1大小的卷积,将尺寸减小到原始维度的1/N，然后直接使用双线性插值上采样恢复到原始图像大小，最后将不同level的特征图进行融合，再使用卷积层进行分类。上图中每个level中使用不同的卷积核，分别为1x1，2x2，3x3和6x6，不同大小的池化模块用于收集不同level的信息。

# 基于ResNet的FCN结构深度监督
这部分没怎么看懂，作者提到论文奖江都产生初始结果，然后再最终损失的情况下继续学习剩下的，从而优化被分为两个部分。

# 实现细节
作者一开头就吐槽了深度学习中细节是魔鬼。  
- 学习策略。学习率使用了‘poly’策略，学习率=基准学习率*$(1-\dfrac{iter}{maxiter})^{power}$,基准学习率和power为0.01，0.9。
- 迭代次数。VOC为30K，ImageNet150K，Cityscapes为90K(迭代这么多次？？)
- 动量和weight decay. 0.9和0.0001
- 数据增强. 随机镜像，随机resize大小0.5-2，随机翻转-10到10度，随机高斯模糊
- batchsize，16，作者说是由于GPU限制的原因。
- auxiliary Loss， 设置权重为0.4，这个loss可以在网上搜到，目前还不知道有什么用。
  
评估方式：主要使用像素精度和平均交并比两种评估方式。
# 结果
1。数据增强提升了1.54IoU/0.72%精度  
2。使用auxiliary loss提高了1.41/0.94  
3。使用PSPnet提高4.45/2.03  
4.更深的网络如ResNet268也提高了精度和mIoU  
最后在多尺度测试中进行测试达到了44.94/81.69
PASCAL VOC数据的结果如下图所示：

<center>
<img src='./image/PSPne results on VOC2012.png'  alt="PSPnet在PASCAL VOC2012测试集结果"  width="100%" height="100%" />    

PSPnet在PASCAL VOC2012测试集结果
</center>

