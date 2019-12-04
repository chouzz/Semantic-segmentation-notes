# 实验结果及笔记记录

## FCN-dataset1-keras.py
最初的实验版本
使用FCN8,训练dataset1,图像大小resize为224*224,类别有12类,优化器使用sgd,损失函数使用categorical_crossentropy,测量方式未accuracy

结果:
其中训练和验证loss值均在0.5附近,且训练和验证losss下降曲线非常接近,可能是由于过拟合的缘故

