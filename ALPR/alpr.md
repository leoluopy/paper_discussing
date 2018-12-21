
# ALPR unconstrained 论文阅读总结和讨论

look for [papers for alpr](./alpr.pdf)
contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.
+ 欢迎watch ，star，实时讨论前沿分享
+ 欢迎加入分享：联系微信：leoluopy

# Overview
+ ![](./overview_eg.png)
+ 来自ECCV2018，提出了一个整套车牌检测，分割，字符识别方案。【很多论文只是这个pipeline其中一部分】
+ 目前大多数方案对于车牌的识别假设车牌正对，或者倾斜角不大。本文提出了WPOD-Net解决车牌倾斜。
+ 本文提供了，倾斜数据、手工标注数据集及合成数据方法（训练集：196张手标数据集） [ 测试集： 102 张困难 倾斜数据集。]
+ 性能上，特定场景和商业持平，非限定场景超过商业系统。
+ 独立测试集表现出强泛化能力。



## 结构综述 【pipeline 总体流程】
+ ![](./full_pipeline.png)
+ 第一步：车辆检测[YOLOV2](../yolo/yolo2/yolo2_discussing.md)
+ 第二步：WPOD-Net 车牌检测，及车牌矫正 （本文重点贡献）
+ 第三步：OCR 车牌识别 （它是巴西车牌，我们这里不关注）


## WPOD-Net 处理流及网络结构
+ resize已经检测出的车辆
+ ![](./resize.png)
+ 参考代码：
+ ![](./code_resize1.png)
+ ![](./code_resize2.png)


## WPOD-Net Loss 设计


## WPOD-Net 数据增广及训练方法


## 整体系统 结果对比

