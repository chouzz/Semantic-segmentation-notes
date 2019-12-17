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

<center>
<img src=./image/Unet-dataset1-acc_val_acc.png alt="训练精度和验证精度"  width="80%" height="80%" />        

训练精度和验证精度
</center>

## IoU度量标准
在从训练集中划分出来56张图片的测试集进行测试,结果如下:
>class 00: #TP=207088, #FP= 28336, #FN=212752, IoU=0.462  
class 01: #TP=574718, #FP=671774, #FN=151598, IoU=0.411  
class 02: #TP=  2538, #FP= 18990, #FN=27423, IoU=0.052  
class 03: #TP=269185, #FP=  9602, #FN=598279, IoU=0.307  
class 04: #TP= 42340, #FP=152351, #FN=101131, IoU=0.143  
class 05: #TP=146064, #FP=106900, #FN=110995, IoU=0.401  
class 06: #TP=  5212, #FP= 23990, #FN=24731, IoU=0.097  
class 07: #TP=  9601, #FP= 29449, #FN=22602, IoU=0.156  
class 08: #TP= 47198, #FP= 31821, #FN=129001, IoU=0.227  
class 09: #TP=  3051, #FP= 19812, #FN=16977, IoU=0.077  
class 10: #TP=   546, #FP=  4375, #FN=11060, IoU=0.034  
class 11: #TP= 45427, #FP=359488, #FN=50339, IoU=0.100  
\_________________  
Mean IoU: 0.206  

对数据集中101张测试集进行测试,结果如下:
>class 00: #TP=   992, #FP=   451, #FN=805370, IoU=0.001  
class 01: #TP=2059859, #FP=1810386, #FN=198984, IoU=0.506  
class 02: #TP=  1701, #FP= 24656, #FN=33821, IoU=0.028  
class 03: #TP= 33586, #FP=  2663, #FN=658302, IoU=0.048  
class 04: #TP= 34269, #FP= 53171, #FN=271791, IoU=0.095  
class 05: #TP=151103, #FP=212529, #FN=203166, IoU=0.267  
class 06: #TP=  5232, #FP= 32890, #FN=86787, IoU=0.042  
class 07: #TP=     0, #FP= 12409, #FN=50173, IoU=0.000  
class 08: #TP= 43352, #FP=108597, #FN=28296, IoU=0.241  
class 09: #TP= 30738, #FP=106011, #FN=28190, IoU=0.186  
class 10: #TP= 17216, #FP=  1832, #FN=230801, IoU=0.069  
class 11: #TP= 20307, #FP=303826, #FN=73740, IoU=0.051  
\_________________  
Mean IoU: 0.128  

## 实验效果
从训练集划分出的测试集效果如下:
<center>
<img src=./image/Unet-dataset1-seg_example_0.png alt="分割示例0"  />        
<img src=./image/Unet-dataset1-seg_example_1.png alt="分割示例1"  />  
<img src=./image/Unet-dataset1-seg_example_2.png alt="分割示例2"  />  
</center>

对数据集中的测试集效果如下所示:
<center>
<img src=./image/Unet-dataset1-test-seg_example_0.png alt="分割示例0"  />        
<img src=./image/Unet-dataset1-test-seg_example_1.png alt="分割示例1"  />  
<img src=./image/Unet-dataset1-test-seg_example_2.png alt="分割示例2"  />  
</center>