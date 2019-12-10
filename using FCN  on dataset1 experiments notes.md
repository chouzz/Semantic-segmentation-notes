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

<center>
<img src=./image/FCN-dataset1-loss_val_loss.png alt="训练损失函数和验证损失函数"  width="80%" height="80%" />        

训练损失函数和验证损失函数
</center>


<center>
<img src=./image/FCN-dataset1-acc_val_acc.png alt="训练精度和验证精度"  width="80%" height="80%" />        

训练精度和验证精度
</center>

## IoU度量标准  
.
平均IoU为0.506,原作者为0.438,但是需要指出的是,该结果是通过对训练集划分0.15的比例为验证集,然后在56张图片的验证集上得到的0.506的mIoU,并不是直接在测试集上得到的mIoU
>class 00: #TP=405776, #FP= 33413, #FN=14064, IoU=0.895  
class 01: #TP=698022, #FP= 81974, #FN=28294, IoU=0.864  
class 02: #TP=     4, #FP=    43, #FN=29957, IoU=0.000  
class 03: #TP=837840, #FP= 25016, #FN=29624, IoU=0.939  
class 04: #TP=114181, #FP= 27535, #FN=29290, IoU=0.668  
class 05: #TP=230089, #FP= 49782, #FN=26970, IoU=0.750  
class 06: #TP=  5146, #FP=  2793, #FN=24797, IoU=0.157  
class 07: #TP= 18735, #FP=  9084, #FN=13468, IoU=0.454  
class 08: #TP=155033, #FP= 29668, #FN=21166, IoU=0.753  
class 09: #TP=   746, #FP=   997, #FN=19282, IoU=0.035  
class 10: #TP=   162, #FP=   203, #FN=11444, IoU=0.014  
class 11: #TP= 62835, #FP= 20779, #FN=32931, IoU=0.539  
\_________________  
Mean IoU: 0.506  

下方为在101张测试集上得到的mIoU数据,平均mIoU为0.317,与验证集有较大的差距
>class 00: #TP=739172, #FP= 38429, #FN=31249, IoU=0.914
class 01: #TP=1770662, #FP=126336, #FN=585376, IoU=0.713  
class 02: #TP=    21, #FP=   442, #FN=32312, IoU=0.001  
class 03: #TP=649511, #FP=374831, #FN=36582, IoU=0.612  
class 04: #TP=134582, #FP=190450, #FN=172959, IoU=0.270  
class 05: #TP=285900, #FP= 69239, #FN=19126, IoU=0.764  
class 06: #TP= 15363, #FP= 12445, #FN=69905, IoU=0.157  
class 07: #TP= 10486, #FP= 17455, #FN=29703, IoU=0.182  
class 08: #TP= 43750, #FP=344540, #FN=20945, IoU=0.107  
class 09: #TP=   918, #FP=  3643, #FN=58233, IoU=0.015  
class 10: #TP=   965, #FP=  1010, #FN=271612, IoU=0.004  
class 11: #TP= 19293, #FP=218333, #FN=69151, IoU=0.063  
\_________________  
Mean IoU: 0.317  



## 实验效果
此为验证集的实验效果,看起来还不错 
<img src=./image/seg_example_0.png alt="分割示例0"  />        
<img src=./image/seg_example_1.png alt="分割示例1"  />  
<img src=./image/seg_example_2.png alt="分割示例2"  />  
</center>


扩展到测试集后,效果就不怎么好了
    <center> 
<img src=./image/fcn-dataset1-test-seg_example_0.png alt="分割示例0"  />        
<img src=./image/fcn-dataset1-test-seg_example_1.png alt="分割示例1"  />  
<img src=./image/fcn-dataset1-test-seg_example_2.png alt="分割示例2"  />  
</center>
# 实验2
## 介绍
实验运行脚本: FCN-dataset1-generator.py
说明:和实验1类似,但是使用批量读取数据的方法使用FCN8,训练dataset1,图像使用随机裁剪到大小为224*224,类别有12类,优化器使用sgd,损失函数使用categorical_crossentropy,测量方式使用accuracy

## 损失和精度 
从图中也可以看出损失降低到了0.5以下,而且训练损失和验证损失区别不大
<center>
<img src=./image/fcn-dataset1-loss_val_loss.png alt="训练损失函数和验证损失函数"  width="80%" height="80%" />        

训练损失函数和验证损失函数
</center>

训练精度和验证精度几乎一致
<center>
<img src=./image/fcn-dataset1-acc_val_acc.png alt="训练精度和验证精度"  width="80%" height="80%" />        

训练精度和验证精度
</center>

## IoU度量标准 


## 实验效果

    <center> 
<img src=./image/FCN-dataset1-seg_example_0.png.png alt="分割示例0"  />        
<img src=./image/fcn-dataset1-seg_example_1.png alt="分割示例1"  />  
<img src=./image/fcn-dataset1-seg_example_2.png alt="分割示例2"  />  
</center>

