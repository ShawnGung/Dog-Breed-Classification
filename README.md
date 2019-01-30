# Dog-Breed-Identification-Kaggle

[Kaggle 狗品种分类比赛](https://www.kaggle.com/c/dog-breed-identification) 

# 环境
- python
- pytorch
- numpy

# 运行
- 下载并解压数据集：https://www.kaggle.com/c/dog-breed-identification/data
- 首先把kaggle的数据放到[data/dog_breed/](data/dog_breed)下
- [features_extract.ipynb](features_extract.ipynb) 导出三种模型输出的特征
- [model_combining.ipynb](model_combining.ipynb) 利用单层神经网络训练合并好的特征,然后在测试集上进行预测

# 感悟
- 通过融合vgg19/resnet152/desnet161的特征,通过训练单层网络训练这些特征达到transfer learning的效果
- 在进行特征融合的时候,时刻保持各种网络特征层输出形状一样
- 如果要做数据增强,注意我们测试集和验证集的transform时候要和训练集的transform分开,后者为了数据增强,前者只是为了调整输出的格式
- 为了更高的准确率,我们可以使用Standford Dog Dataset来增加数据,可以到达接近0的loss

# 模型融合好处与坏处
- 好处:计算快,前期不需要反向传播,另外能很好利用各种不同结构网络学习到的知识
- 坏处:目前实现方法,把特征存到本地,所以如果一旦数据增强(flip之类)会改变整体数据的分布,丢失掉原始数据(解决办法:多进行几次特征提取(同时数据增强),这样相当于扩大数据集)

# 训练Epoch,验证集的准确率和损失

epoch | train_loss | valid loss | train_acc | valid_acc | time
----|---- |---- |---- |---- |---- |
epoch 5 | train loss : 0.8753 | valid loss : 0.9557 | train_acc : 0.9168 | valid_acc : 0.8815 | time :0.4157 sec
epoch 10 | train loss : 0.4923 | valid loss : 0.5814 | train_acc : 0.9380 | valid_acc : 0.8932 | time :1.5548 sec
epoch 15 | train loss : 0.3722 | valid loss : 0.4645 | train_acc : 0.9461 | valid_acc : 0.8971 | time :0.3535 sec
epoch 20 | train loss : 0.3102 | valid loss : 0.4431 | train_acc : 0.9511 | valid_acc : 0.8867 | time :0.8151 sec
epoch 25 | train loss : 0.2710 | valid loss : 0.4020 | train_acc : 0.9560 | valid_acc : 0.8880 | time :0.6144 sec
epoch 30 | train loss : 0.2428 | valid loss : 0.3784 | train_acc : 0.9603 | valid_acc : 0.8867 | time :1.5378 sec
epoch 35 | train loss : 0.2213 | valid loss : 0.3533 | train_acc : 0.9641 | valid_acc : 0.9010 | time :0.3081 sec
epoch 40 | train loss : 0.2033 | valid loss : 0.3389 | train_acc : 0.9670 | valid_acc : 0.9010 | time :0.3081 sec
epoch 45 | train loss : 0.1884 | valid loss : 0.3434 | train_acc : 0.9698 | valid_acc : 0.8971 | time :0.3146 sec
epoch 50 | train loss : 0.1762 | valid loss : 0.3516 | train_acc : 0.9723 | valid_acc : 0.8971 | time :0.3885 sec
epoch 55 | train loss : 0.1656 | valid loss : 0.3196 | train_acc : 0.9742 | valid_acc : 0.9036 | time :0.7152 sec
epoch 60 | train loss : 0.1562 | valid loss : 0.3144 | train_acc : 0.9763 | valid_acc : 0.9036 | time :1.4714 sec
epoch 65 | train loss : 0.1477 | valid loss : 0.3222 | train_acc : 0.9782 | valid_acc : 0.8984 | time :0.3500 sec
epoch 70 | train loss : 0.1405 | valid loss : 0.3129 | train_acc : 0.9794 | valid_acc : 0.9076 | time :0.3506 sec
epoch 75 | train loss : 0.1337 | valid loss : 0.3226 | train_acc : 0.9808 | valid_acc : 0.8971 | time :0.4349 sec
epoch 80 | train loss : 0.1280 | valid loss : 0.3219 | train_acc : 0.9824 | valid_acc : 0.8958 | time :1.5441 sec
epoch 85 | train loss : 0.1218 | valid loss : 0.3030 | train_acc : 0.9837 | valid_acc : 0.9036 | time :0.4750 sec
epoch 90 | train loss : 0.1166 | valid loss : 0.3260 | train_acc : 0.9849 | valid_acc : 0.8971 | time :0.3510 sec
epoch 95 | train loss : 0.1118 | valid loss : 0.3025 | train_acc : 0.9861 | valid_acc : 0.8984 | time :0.4335 sec
epoch 100 | train loss : 0.1074 | valid loss : 0.3153 | train_acc : 0.9870 | valid_acc : 0.8958 | time :1.2307 sec


# 感谢
感谢[ypw](https://github.com/ypwhs/DogBreed_gluon) and [fiercex](https://fiercex.github.io/post/gluon_kaggle/)的代码和思想分享,本文利用pytorch来复现

