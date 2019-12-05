- [语义分割模型笔记](#%e8%af%ad%e4%b9%89%e5%88%86%e5%89%b2%e6%a8%a1%e5%9e%8b%e7%ac%94%e8%ae%b0)
  - [vgg16(very deep convolutional networks for large-scale image recognition)](#vgg16very-deep-convolutional-networks-for-large-scale-image-recognition)
# 语义分割模型笔记

## vgg16(very deep convolutional networks for large-scale image recognition)
一篇图像识别的开山之作,vgg网络,摘要就说达到了他们的方法达到了state-of-the-art...但是其实后面还有很多算法出现了.
这篇文章中设置了很多3x3卷积来代替7x7的卷积,许多参数设置都被后来的文章或者实验所应用,例如l2惩罚系数设置为$5*10^{-4}$,dropout设置为0.5,验证集精度不再提高时学习率减少10倍等等,都是来自于这篇文章.  

除此之外,这篇文章还对图像进行预处理,包括处理成固定大小的224x224,随机垂直翻转和随机RGB色彩偏移.


[相关笔记1](http://deanhan.com/2018/07/26/vgg16/)
