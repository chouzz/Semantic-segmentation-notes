- [实验结果及笔记记录](#%e5%ae%9e%e9%aa%8c%e7%bb%93%e6%9e%9c%e5%8f%8a%e7%ac%94%e8%ae%b0%e8%ae%b0%e5%bd%95)
- [实验1](#%e5%ae%9e%e9%aa%8c1)
  - [介绍](#%e4%bb%8b%e7%bb%8d)
  - [损失和精度](#%e6%8d%9f%e5%a4%b1%e5%92%8c%e7%b2%be%e5%ba%a6)
  - [IoU度量标准](#iou%e5%ba%a6%e9%87%8f%e6%a0%87%e5%87%86)
  - [实验效果](#%e5%ae%9e%e9%aa%8c%e6%95%88%e6%9e%9c)
# 实验结果及笔记记录

# 实验1

## 介绍
实验运行脚本: Unet-dataset1.py 
说明:使用Unet模型训练dataset1,图像随机剪裁为224*224,类别有12类,优化器使用sgd,损失函数使用categorical_crossentropy,测量方式使用accuracy
## 损失和精度 
可以看到损失下降到了0.4以下,精度也提高到了0.9以上,但是实际的IoU和预测情况却不是很理想
<center>
<img src=./image/Unet-dataset1-loss_val_loss.png alt="训练损失函数和验证损失函数"  width="80%" height="80%" />        

训练损失函数和验证损失函数
</center>
而对于训练精度和验证精度其实和loss是差不多的,有可能训练批数还不太够,这里只训练了200个epochs   
<center>
<img src=./image/Unet-dataset1-acc_val_acc.png alt="训练精度和验证精度"  width="80%" height="80%" />        

训练精度和验证精度
</center>

## IoU度量标准
平均IoU为0.211
>class 00: #TP=246734, #FP= 38910, #FN=173106, IoU=0.538  
class 01: #TP=566080, #FP=561078, #FN=160236, IoU=0.440  
class 02: #TP=  2296, #FP= 15739, #FN=27665, IoU=0.050  
class 03: #TP=267033, #FP=  8703, #FN=600431, IoU=0.305  
class 04: #TP= 32572, #FP=144479, #FN=110899, IoU=0.113  
class 05: #TP=189094, #FP=214809, #FN=67965, IoU=0.401  
class 06: #TP=  6107, #FP= 28735, #FN=23836, IoU=0.104  
class 07: #TP=  8894, #FP=  9831, #FN=23309, IoU=0.212  
class 08: #TP= 49335, #FP= 26853, #FN=126864, IoU=0.243  
class 09: #TP=  1323, #FP=  5656, #FN=18705, IoU=0.052  
class 10: #TP=     9, #FP=  2790, #FN=11597, IoU=0.001  
class 11: #TP= 33984, #FP=348812, #FN=61782, IoU=0.076  
\_________________  
Mean IoU: 0.211  

## 实验效果
<center>
<img src=./image/Unet-dataset1-seg_example_0.png alt="分割示例0"  />        
<img src=./image/Unet-dataset1-seg_example_1.png alt="分割示例1"  />  
<img src=./image/Unet-dataset1-seg_example_2.png alt="分割示例2"  />  
</center>