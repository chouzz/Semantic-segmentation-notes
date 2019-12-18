- [深度学习中的损失函数和优化器(loss function and optimizer)](#%e6%b7%b1%e5%ba%a6%e5%ad%a6%e4%b9%a0%e4%b8%ad%e7%9a%84%e6%8d%9f%e5%a4%b1%e5%87%bd%e6%95%b0%e5%92%8c%e4%bc%98%e5%8c%96%e5%99%a8loss-function-and-optimizer)
- [损失函数和优化器](#%e6%8d%9f%e5%a4%b1%e5%87%bd%e6%95%b0%e5%92%8c%e4%bc%98%e5%8c%96%e5%99%a8)
- [常见的损失函数](#%e5%b8%b8%e8%a7%81%e7%9a%84%e6%8d%9f%e5%a4%b1%e5%87%bd%e6%95%b0)
- [常见的优化器函数](#%e5%b8%b8%e8%a7%81%e7%9a%84%e4%bc%98%e5%8c%96%e5%99%a8%e5%87%bd%e6%95%b0)
  - [相关链接](#%e7%9b%b8%e5%85%b3%e9%93%be%e6%8e%a5)
# 深度学习中的损失函数和优化器(loss function and optimizer)

# 损失函数和优化器
损失函数（loss function）是用来估量模型的预测值f(x)与真实值Y的不一致程度，损失函数越小，一般就代表模型的鲁棒性越好，正是损失函数指导了模型的学习

优化器(optimizer)是在有了损失函数之后，使用优化算法将其最小化，在优化过程中，损失函数也成称为目标函数(objective function)，在动手学深度学习一章提到了，其实优化器是优化训练误差，也就是在训练过程中产生的误差，而深度学习最终的目标是为了降低泛化误差，这里优化器是有一定限制的，为了求得最小化目标函数的数值解，将通过优化算法有限次迭代模型参数来尽可能降低损失函数的值。


# 常见的损失函数
  
mean_absolute_error  
mean_absolute_percentage_error  
mean_squared_logarithmic_error  
squared_hinge  
hinge  
categorical_hinge  
logcosh  
huber_loss  
categorical_crossentropy  
sparse_categorical_crossentropy  
binary_crossentropy  
kullback_leibler_divergence  
poisson  
cosine_proximity  
is_categorical_crossentropy  
以上来源于keras内置的损失函数
# 常见的优化器函数
SGD  
RMSprop  
Adagrad  
Adadelta  
Adam  
Adamax  
Nadam  
## 相关链接
https://www.zhihu.com/question/317383780/answer/631866229
介绍了分类和回归中常见的损失函数，但是并没有说清楚原理，只给出了公式

***
https://blog.csdn.net/qq_41997920/article/details/88693888
给出了pytorch中的损失函数和优化器