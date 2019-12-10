- [实验结果及笔记记录](#%e5%ae%9e%e9%aa%8c%e7%bb%93%e6%9e%9c%e5%8f%8a%e7%ac%94%e8%ae%b0%e8%ae%b0%e5%bd%95)
- [实验1](#%e5%ae%9e%e9%aa%8c1)
  - [介绍](#%e4%bb%8b%e7%bb%8d)
  - [损失和精度](#%e6%8d%9f%e5%a4%b1%e5%92%8c%e7%b2%be%e5%ba%a6)
  - [IoU度量标准](#iou%e5%ba%a6%e9%87%8f%e6%a0%87%e5%87%86)
  - [实验效果](#%e5%ae%9e%e9%aa%8c%e6%95%88%e6%9e%9c)
- [实验2](#%e5%ae%9e%e9%aa%8c2)
  - [介绍](#%e4%bb%8b%e7%bb%8d-1)
  - [损失和精度](#%e6%8d%9f%e5%a4%b1%e5%92%8c%e7%b2%be%e5%ba%a6-1)
  - [IoU度量标准](#iou%e5%ba%a6%e9%87%8f%e6%a0%87%e5%87%86-1)
  - [实验效果](#%e5%ae%9e%e9%aa%8c%e6%95%88%e6%9e%9c-1)
# 实验结果及笔记记录

# 实验1
## 介绍
实验运行脚本: FCN-dataset1-keras.py  
说明:最初的实验版本,使用FCN8,训练dataset1,图像大小resize为224*224,类别有12类,优化器使用sgd,损失函数使用categorical_crossentropy,测量方式使用accuracy

## 损失和精度 
其中训练和验证loss值均在0.5附近,且训练和验证losss下降曲线非常接近,可能是由于过拟合的缘故

<center>
<img src=./image/loss_val_loss.png alt="训练损失函数和验证损失函数"  width="80%" height="80%" />        

训练损失函数和验证损失函数
</center>
而对于训练精度和验证精度其实和loss是差不多的,有可能训练批数还不太够,这里只训练了200个epochs   
<center>
<img src=./image/acc_val_acc.png alt="训练精度和验证精度"  width="80%" height="80%" />        

训练精度和验证精度
</center>

## IoU度量标准  
训练的平均IoU为0.418,而原作者为0.438,略低于原作者.
>class 00: #TP=409327, #FP= 48078, #FN=10513, IoU=0.875  
class 01: #TP=660072, #FP= 71314, #FN=66244, IoU=0.828    
class 02: #TP=     6, #FP=    96, #FN=29955, IoU=0.000  
class 03: #TP=845554, #FP= 72664, #FN=21910, IoU=0.899  
class 04: #TP= 99666, #FP= 31304, #FN=43805, IoU=0.570  
class 05: #TP=232939, #FP= 77505, #FN=24120, IoU=0.696  
class 06: #TP=  2094, #FP=  2116, #FN=27849, IoU=0.065  
class 07: #TP= 18466, #FP= 17340, #FN=13737, IoU=0.373  
class 08: #TP=157664, #FP= 60566, #FN=18535, IoU=0.666  
class 09: #TP=   895, #FP=  2190, #FN=19133, IoU=0.040    
class 10: #TP=     0, #FP=     0, #FN=11606, IoU=0.000   
class 11: #TP=     0, #FP=     0, #FN=95766, IoU=0.000  
\________________  
Mean IoU: 0.418

这里的class10和class11可能还有点问题,和[原作者的实验](https://fairyonice.github.io/Learn-about-Fully-Convolutional-Networks-for-semantic-segmentation.html#Visualize-the-model-performance)的区别有点大.

## 实验效果
精细度还是不够好
<img src=./image/seg_example_0.png alt="分割示例0"  />        
<img src=./image/seg_example_1.png alt="分割示例1"  />  
<img src=./image/seg_example_2.png alt="分割示例2"  />  
</center>

# 实验2
## 介绍
实验运行脚本: FCN-dataset1-generator.py
说明:和实验1类似,但是使用批量读取数据的方法使用FCN8,训练dataset1,图像使用随机裁剪到大小为224*224,类别有12类,优化器使用sgd,损失函数使用categorical_crossentropy,测量方式使用accuracy

## 损失和精度 
从图中也可以看出损失降低到了0.5以下,而且训练损失和验证损失区别不大
<center>
<img src=./image/fcn-dataset1-generator-loss_val_loss.png alt="训练损失函数和验证损失函数"  width="80%" height="80%" />        

训练损失函数和验证损失函数
</center>

训练精度和验证精度几乎一致
<center>
<img src=./image/fcn-dataset1-generator-acc_val_acc.png alt="训练精度和验证精度"  width="80%" height="80%" />        

训练精度和验证精度
</center>

## IoU度量标准 
平均IoU为0.130


>class 00: #TP=  2244, #FP=  2273, #FN=792370, IoU=0.003  
class 01: #TP=2218862, #FP=1533372, #FN=74457, IoU=0.580   
class 02: #TP=     0, #FP=    17, #FN=34286, IoU=0.000  
class 03: #TP=170441, #FP=  6488, #FN=529738, IoU=0.241  
class 04: #TP=135559, #FP=279023, #FN=153502, IoU=0.239  
class 05: #TP=126385, #FP= 20534, #FN=213285, IoU=0.351  
class 06: #TP=  2718, #FP=  4021, #FN=89392, IoU=0.028  
class 07: #TP=    51, #FP=   898, #FN=49372, IoU=0.001  
class 08: #TP= 34186, #FP=394291, #FN=31247, IoU=0.074  
class 09: #TP=  1155, #FP= 17563, #FN=63896, IoU=0.014  
class 10: #TP=   164, #FP=    77, #FN=252605, IoU=0.001  
class 11: #TP=  4695, #FP=112759, #FN=87166, IoU=0.023  
\_________________  
Mean IoU: 0.130

## 实验效果

<img src=./image/fcn-dataset1-generator-seg_example_0.png alt="分割示例0"  />        
<img src=./image/fcn-dataset1-generator-seg_example_1.png alt="分割示例1"  />  
<img src=./image/fcn-dataset1-generator-seg_example_2.png alt="分割示例2"  />  
</center>
