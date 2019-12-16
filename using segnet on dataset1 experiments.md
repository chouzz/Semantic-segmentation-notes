- [实验结果及笔记记录](#%e5%ae%9e%e9%aa%8c%e7%bb%93%e6%9e%9c%e5%8f%8a%e7%ac%94%e8%ae%b0%e8%ae%b0%e5%bd%95)
- [实验1](#%e5%ae%9e%e9%aa%8c1)
  - [介绍](#%e4%bb%8b%e7%bb%8d)
  - [损失和精度](#%e6%8d%9f%e5%a4%b1%e5%92%8c%e7%b2%be%e5%ba%a6)
  - [IoU交并比](#iou%e4%ba%a4%e5%b9%b6%e6%af%94)
  - [实验效果](#%e5%ae%9e%e9%aa%8c%e6%95%88%e6%9e%9c)
# 实验结果及笔记记录

# 实验1
## 介绍
SegNet实验,Segnet在原论文中是一种分类的网络,其最后一层的网络为softmax进行分类,这里改为了1x1的卷积,然后生成的12个类别,最终输出分割图像.
segnet和Unet非常相似,它在上采样过程中不同


## 损失和精度 
损失和精度如下图所示
<center>
<img src=./image/SegNet-dataset1-loss_val_loss.png alt="训练损失函数和验证损失函数"  width="80%" height="80%" />        

训练损失函数和验证损失函数
</center>


<center>
<img src=./image/SegNet-dataset1-acc_val_acc.png alt="训练精度和验证精度"  width="80%" height="80%" />        

训练精度和验证精度
</center>

## IoU交并比
对从训练集划分出来的测试集进行IoU计算得到结果如下:

>class 00: #TP=396866, #FP= 35190, #FN=22974, IoU=0.872  
class 01: #TP=649199, #FP= 79534, #FN=77117, IoU=0.806  
class 02: #TP=   335, #FP=  1098, #FN=29626, IoU=0.011  
class 03: #TP=773716, #FP= 39785, #FN=93748, IoU=0.853  
class 04: #TP= 96268, #FP= 49661, #FN=47203, IoU=0.498  
class 05: #TP=205857, #FP= 46541, #FN=51202, IoU=0.678  
class 06: #TP=  3720, #FP=  7565, #FN=26223, IoU=0.099  
class 07: #TP= 12236, #FP= 15665, #FN=19967, IoU=0.256  
class 08: #TP=137959, #FP= 54696, #FN=38240, IoU=0.597  
class 09: #TP=  4406, #FP= 16405, #FN=15622, IoU=0.121  
class 10: #TP=   471, #FP=  1367, #FN=11135, IoU=0.036  
class 11: #TP= 55171, #FP=126145, #FN=40595, IoU=0.249  
\_________________  
Mean IoU: 0.423  

对数据集内的101张测试集进行测试,结果如下:
>class 00: #TP=761248, #FP= 18832, #FN=67356, IoU=0.898  
class 01: #TP=1865337, #FP=133028, #FN=377772, IoU=0.785  
class 02: #TP=    25, #FP=  1212, #FN=30935, IoU=0.001  
class 03: #TP=569637, #FP= 31474, #FN=107878, IoU=0.803  
class 04: #TP=247561, #FP=158925, #FN=33435, IoU=0.563  
class 05: #TP=361100, #FP= 48711, #FN=28857, IoU=0.823  
class 06: #TP= 31421, #FP= 53647, #FN=53827, IoU=0.226  
class 07: #TP=  4589, #FP= 27220, #FN=55314, IoU=0.053  
class 08: #TP= 44515, #FP= 70376, #FN=22209, IoU=0.325  
class 09: #TP= 42990, #FP=204100, #FN=14303, IoU=0.164  
class 10: #TP= 15469, #FP=  4948, #FN=238534, IoU=0.060  
class 11: #TP= 56129, #FP=315282, #FN=37335, IoU=0.137  
\_________________
Mean IoU: 0.403


## 实验效果
对从训练集划分出的测试集进行测试,得到结果如下:
<center>
<img src=./image/SegNet-dataset1-seg_example_0.png alt="分割示例0"  />        
<img src=./image/SegNet-dataset1-seg_example_1.png alt="分割示例1"  />  
<img src=./image/SegNet-dataset1-seg_example_2.png alt="分割示例2"  />  
</center>

***     
对包含101张图片测试集进行测试,得到的结果如下图所示:
<center>
<img src=./image/SegNet-dataset1-test-seg_example_0.png alt="分割示例0"  />        
<img src=./image/SegNet-dataset1-test-seg_example_1.png alt="分割示例1"  />  
<img src=./image/SegNet-dataset1-test-seg_example_2.png alt="分割示例2"  />  
</center>
