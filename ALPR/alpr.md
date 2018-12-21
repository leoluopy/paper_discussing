
# ALPR unconstrained 论文阅读总结和讨论

look for [papers for alpr](./alpr.pdf)
contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.
+ 欢迎watch ，star，实时讨论前沿分享
+ 欢迎加入分享：联系微信：leoluopy

# Overview

+ 来自ECCV2018，提出了一个整套车牌检测，分割，字符识别方案。【很多论文只是这个pipeline其中一部分】
+ 目前大多数方案对于车牌的识别假设车牌正对，或者倾斜角不大。本文提出了WPOD-Net解决车牌倾斜。
+ 本文提供了，倾斜数据、手工标注数据集及合成数据方法（训练集：196张手标数据集） [ 测试集： 102 张困难 倾斜数据集。]
+ 性能上，特定场景和商业持平，非限定场景超过商业系统。
+ 独立测试集表现出强泛化能力。



## 结构综述


