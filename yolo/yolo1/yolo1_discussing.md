
# YOLO V1 

look for [papers for yolo1](https://github.com/leoluopy/paper_discussing/blob/master/yolo/yolo1/yolo_1.pdf)


# Overview

+ 首个OneStage网络（SSD也是）regression思路
+ 学习特征是泛化能力特别强特征(在艺术画上泛华能力仍然较强，对比同时期RCNN，RCNN在艺术画识别能力大幅下降)
+ 速度极快（多个子类型网络达到实时）

摒弃滑窗或候选框，直接全局回归目标位置和分类



预测置信度计算公式：

![](./fromula_pre.png)

对应类概率 × 有无对象概率 × 预测box和真实box比值 = 最终预测置信度


