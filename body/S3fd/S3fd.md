

# S3fd 核心点笔记

looking for papers for [S3fd](https://arxiv.org/abs/1708.05237)

contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.欢迎watch ，star.

# Overview
+ 人脸检测领域作为通用目标检测中特定目标的检测，目前有很大的发展，但是在小目标和非标准困难目标的检测中仍然是挑战，本文在相应的难题中
从改善anchor着眼提出了以下几点改善，大大提高了recall
+ 从感受野均匀分布，anchor大小均匀分布重新设计了anchor分布规则
+ 训练中对anchor匹配做了相应的补偿和过滤，使得原本没有学习空间的anchor有更多的学习机会
+ 在anchor分布改善后出现的大量微小负样本anchor,本文使用了maxOut分类方式进行抑制也对recall提高做出了贡献

# 效果描述
+ ![](./retAFW.png)
> AFW上的precision,recall指标表现
+ ![](./retPASCAL.png)
> PASCAL上的precision,recall指标表现
+ ![](./retFDDB.png)
> FDDB上的ROC[TPR/FPR]指标表现
+ ![](./retWIDERFACE.png)
> WIDERFACE上各个子数据集的precesion,recall指标表现

> PR曲线物理意义：在越来越低的漏检率时，正确率有多少　　【主要目标，对一定情况下，漏多少】

> ROC曲线物理意义：在一定的错误次数或者错误率时，正确率或者正确次数是多少　【主要目标，对一定情况下，有多次错误出现】

# 核心点叙述
+ ![](./problemOfanchor.png)
+ 为解决传统目标检测领域存在的问题，首先本文明确了anchor方法存在的问题：
    + 在小人脸情况下，特征在anchor中的提取不足
    + 在anchor一定情况下，和目标人脸不匹配
    + 在设计小anchor时，在一定大小的特征图中，会出现异常多的负样本，因为他们感受野下的目标都不是人脸
+ ![](./receptiveF_achor.png)
+ ![](./scale_equitable_anchor.png)
+ 解决anchor问题，本文提出了第一步：均匀的分布人脸anchor
    + 如上图所示在各个不同的特征图上，不同的Anchor尺寸，按照 N/4滑动，均分分布在特征图上
    + N 是anchor的尺寸
    + RF是感受野，这里指当前做回归的特征图的一部分
+ ![](./anchorNum.png)
+ 上表对应了在不同的的预测特征图上对应的anchor数量，Scale为16时【也即是anchor为16】时，anchor最多。

+ 解决anchor问题，本文提出了第二步：anchor匹配补偿
    + 原有anchor匹配阈值从0.5降低至0.35,并对anchor匹配成功的目标GT求得平均值。
    + 取到anchor匹配过程中0.1到0.35之间的anchor,并排序，取TopN的anchor作为匹配结果,N就是刚才算到的平均值
    + 这样一来有更多的anchor有相应的学习机会，同时匹配度低的anchor中有参考意义的anchor也能学习到特征

+ ![](./maxOutAndmatchStrategy.png)
+ 解决anchor问题，本文提出了第三步：label max-Out处理
    + 实际上这种处理就是加大在分类器训练过程中人脸label的权重 [如上图所示]
> max-out background 参考代码
```
max_conf, _ = torch.max(conf_x[:, 0:3, :, :], dim=1, keepdim=True)
第一维是batchSize ，第二维是maxOut的label,第三维第四维是特征图尺寸.
```

+ ![](./ablationStudy.png)
+ 消融学习结论如上
    + 均匀anchor分布贡献最大,maxOut和匹配补偿都有相应的贡献
    + F: anchor均匀分布
    + S: anchor匹配补偿
    + M: 分类器maxOut策略
# 模型结构叙述
+ ![](./netWork.png)
+ 基础网络左上角所示，是VGG16是主要的特征提取器，extraLayers也能做一定的特征提取
+ 在中间是预测layer主要目的是使用这些在不同scale上提取到的特征进行目标回归和分类。
+ 第一个预测层中加了上文所说的maxOut方法

# 训练Loss设计
+ ![](LossFun.png)
+ cls是分类器Loss，被正样本和负样本同时归一化
+ reg是位置Loss,被正样本归一化





