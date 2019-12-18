- [实验结果及笔记记录](#%e5%ae%9e%e9%aa%8c%e7%bb%93%e6%9e%9c%e5%8f%8a%e7%ac%94%e8%ae%b0%e8%ae%b0%e5%bd%95)
- [实验1](#%e5%ae%9e%e9%aa%8c1)
  - [介绍](#%e4%bb%8b%e7%bb%8d)
  - [训练参数设置](#%e8%ae%ad%e7%bb%83%e5%8f%82%e6%95%b0%e8%ae%be%e7%bd%ae)
  - [损失和精度](#%e6%8d%9f%e5%a4%b1%e5%92%8c%e7%b2%be%e5%ba%a6)
  - [IoU交并比](#iou%e4%ba%a4%e5%b9%b6%e6%af%94)
  - [实验效果](#%e5%ae%9e%e9%aa%8c%e6%95%88%e6%9e%9c)
# 实验结果及笔记记录

# 实验1
## 介绍
PSPnet,其主要贡献是提出了金字塔池化模块，能够利用多尺度信息，更好的理解图像中的场景信息。

## 训练参数设置
- train_batch_size: 16
- val_batch_size: 16
- crop_size: (224, 224)
- nClasses: 12
- resnet_layers: 50
- optimizer: SGD,lr=1E-2, decay=5**(-4), momentum=0.9 nesterov=True
- loss: categorical_crossentropy
- metrics: accuracy
- earlyStopping: monitor='val_loss', patience=15, mode='auto'
- epoches: 300


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


对数据集内的101张测试集进行测试,结果如下:



## 实验效果


***     
对包含101张图片测试集进行测试,得到的结果如下图所示:
<center>
<img src=./image/SegNet-dataset1-test-seg_example_0.png alt="分割示例0"  />        
<img src=./image/SegNet-dataset1-test-seg_example_1.png alt="分割示例1"  />  
<img src=./image/SegNet-dataset1-test-seg_example_2.png alt="分割示例2"  />  
</center>
