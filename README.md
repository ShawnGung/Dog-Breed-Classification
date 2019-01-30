# Dog-Breed-Identification-Kaggle

[Kaggle](https://www.kaggle.com/c/dog-breed-identification) 

# 环境
- python
- pytorch
- numpy

# 感悟
- 通过融合vgg19/resnet152/desnet161的特征,通过训练单层网络训练这些特征达到transfer learning的效果
- 在进行特征融合的时候,时刻保持各种网络特征层输出形状一样
- 如果要做数据增强,注意我们测试集和验证集的transform时候要和训练集的transform分开,后者为了数据增强,前者只是为了调整输出的格式
- 为了更高的准确率,我们可以使用Standford Dog Dataset来增加数据,可以到达接近0的loss

# 模型融合好处与坏处
- 好处:计算快,前期不需要反向传播,另外能很好利用各种不同结构网络学习到的知识
- 坏处:目前实现方法,把特征存到本地,所以如果一旦数据增强(flip之类)会改变整体数据的分布,丢失掉原始数据(解决办法:多进行几次特征提取(同时数据增强),这样相当于扩大数据集)


# 感谢
感谢[ypw](https://github.com/ypwhs/DogBreed_gluon) and [fiercex](https://fiercex.github.io/post/gluon_kaggle/)的代码和思想分享,本文利用pytorch来复现

