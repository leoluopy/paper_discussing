

# HopeNet 核心点解析

looking for papers for [HopeNet](https://arxiv.org/abs/1710.00925)

contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.欢迎watch ，star.
+ 微信号：leoluopy，如有疑问，欢迎交流，得文时浅，或有纰漏，请不吝指教。

<img width="200" height="200" src="https://github.com/leoluopy/paper_discussing/blob/master/wechat_id.jpeg"/>


# Overview
+ ![](./effecient1.png)
+ 在这之前人脸姿态的估计基于已经检测好的人脸关键点，或者结合深度信息来估计人脸姿态；这样带来的缺点是或者检测精度
严重依赖关键点的精度，效果受到图像模糊度重大影响，或者需要比较昂贵的深度数据重建3DMM模型。本文提出了一种直接使用特征图回归
 人脸各个方向角度的方法，即三个角度使用共同特征提取后面接三个不同FC+softmax+期望转换层，回归得到不同角度
+ 为了使模型得到良好的收敛，文章设计了双loss结构，crossEntropy负责控制回归粒度比较粗的角度基点，MSE负责控制回归基于刚才角度基点的
期望调整
+ 在数据增广方面，这个模型生成了人脸姿态数据和各种角度的模糊人脸数据可以大幅度提升模型的精确度

# 效果描述
![](./effecient2.png)

# 模型结构叙述
![](./structure.png)

分层
Outscore= 

# Loss及训练方法
![](./loss.png)
+ H是crossEntropy交叉熵
+ Loss 分为两部分crossEntropy用于控制分类回归角度的角度基点，MSE用于控制基于角度基点的期望调整
![](lowResolutionStudy.png)




