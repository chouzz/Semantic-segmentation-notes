# github项目中FCN实验笔记

# 实验项目
https://github.com/aurora95/Keras-FCN

# 实验环境
Ubuntu14.04
cuda8.0
tensorflow-gpu1.4.1
keras2.0.8

keras和tensorflow版本有点低，故在gitclone之后需要对原版本进行修改一部分，特别是数据预处理的那部分，需要手动修改Iterator类。
# 实验次数及过程
修改Iterator类，使代码能够适应keras2.0.8版本，然后将数据集修改为VOC2012数据集，原代码使用的不仅仅有VOC2012，还有VOC2012扩展数据集，这里先对VOC2012数据集进行实验，在得出基本的结果再进行其他的实验。
1. 和原代码一样，不使用验证集进行训练，不使用预训练权重文件，然后在评估文件中将targetsize改为320，320，在预测之前使用cv2.resize来改变测试集图像的大小，最后得到mIoU为0.12，结果自然惨不忍睹。
2. 将验证集也加入到训练中去，在评估文件中将targetsize改为512，512，去除cv2.resize函数，不足512的部分使用np.lib.pad填充为0，然后进行预测评估，最后得到mIoU为0.22，预测效果同样很差。
3. 
