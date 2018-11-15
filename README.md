# miniDeepFrame
手动实现mini深度学习框架，主要精力不放在运算优化上，仅体会原理

#### 相关博客
[『计算机视觉』mini深度学习框架实现](https://www.cnblogs.com/hellcat/p/9963383.html)<br>
[『TensorFlow』卷积层、池化层详解](https://www.cnblogs.com/hellcat/p/7850048.html)<br>
[『科学计算』全连接层、均方误差、激活函数实现](https://www.cnblogs.com/hellcat/p/7172950.html)<br>

#### 文件介绍
`Layer.py`     层 class，已实现：全连接层，卷积层，平均池化层<br>
`Loss.py`      损失函数 class，已实现：均方误差损失函数<br>
`Activate.py`  激活函数 class，已实现：sigmoid、tanh、relu<br>
`test.py`      训练测试代码<br>
注意，主流框架对于卷积相关层的实现都是基于矩阵乘法运算，而非这里的多层for循环
#### 测试输出
我们此时不对层函数进行封装，仅仅实现了最简单的前向传播、反向传播、参数获取几个功能，利用这些功能，我们已经可以实现一个最简单的神经网络，
```
    声明并初始化各层class的实例，这会使得各个实例初始化可学习参数
    （【注】一般的框架会在运行时，即第一次前向传播时才初始化参数，本demo由于是动态的，所以没必要这样写）
    进入循环体：
    　　获取数据，向前传播，计算损失函数&损失函数的梯度
    　　向后传播，获取各个参数的梯度
    　　对参数循环，利用参数梯度更新参数
```
在test.py中，我们使用tensorflow的接口，下载并读取mnist数据集，然后训练一个10分类的分类器，观察收敛过程。实际训练并查看中间输出可以看见，最开始几次训练的损失函数下降的极快，相应的梯度值如果添加了中间的输出也会极大（10^3量级，对应的参数初始化为-1~1之间），下图展示了截掉了前四次迭代之后的Loss，能够更好的展示收敛细节（未截取版本可以去博客看）：
![](https://img2018.cnblogs.com/blog/1161096/201811/1161096-20181115144133763-312913842.png)
