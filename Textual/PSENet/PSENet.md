

# LFFD 核心点笔记

looking for papers for [PSE](https://arxiv.org/abs/1806.02559)

contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.欢迎watch ，star.
+ 微信号：leoluopy，如有疑问，欢迎交流，得文时浅，或有纰漏，请不吝指教。

<img width="200" height="200" src="https://github.com/leoluopy/paper_discussing/blob/master/wechat_id.jpeg"/>


# Overview
![](./overview_effe.png)
+ 在字符检测领域，传统的矩形框方法难以检测到不规则形状的文字，但在自然环境中这种情况广泛存在，因此基于分割的字符检测方法应运而生
    + 基于分割的字符检测方法在任意形状文字检测上取得了良好效果，但是在字符间距很小时容易出现粘连问题。本文介绍的方法基于以下贡献点解决该问题
    + 设计了多个尺度的特征图卷积核，从最小尺寸的特征图卷积核依次膨胀得到最后结果解决了粘连问题
    + 使用图像腐蚀方法生成了若干训练数据，不需要单独标注
    + 在各个数据集都取得了state-of-art成绩

# 效果描述
![](./ret_of_curve.png)
![](./compareToother.png)
+ 由图可见在IC15,IC17,CTW1500上，PSENet在Precesion, Recall, F1-Score都取得了不错的成绩。


# 模型结构叙述
![](./netWork.png)
+ PSE网络结构受FPN启发，首先经过若干卷积提取多个尺度的特征图，这里是４个尺度的特征图(P5 P4 P3 P2)
+ 特征图经过上下采样得到融合后的特征图F
+ 单个特征图F被采样处理为多个尺度的特征图卷积核（Sn Sn-1 S1）
+ 在这些特征图卷积核上做最后的分割预测

# 分割预测的膨胀过程
![](./pipeline.png)
+ 在多个特征图预测得到各自尺度的分割结果后，这些结果需要融合以下是融合过程的概述：
    + 从最小尺度的特征图结果开始融合，依次往最大特征图运算
    + 如果有分割结果冲突，遵从先到先占位原则进行融合 


## 消融研究
![](./ablation.png)
+ m : 缩放比例(最小/原始)
+ n : 预测特征图个数

# 训练及Loss设计
## label生产
![](./shrink_formula.png)
![](./shrinkLabel.png)

## Loss
![](./loss_all.png)
+  

![](./loss_seg1.png)
![](./loss_seg2.png)
![](./loss_shrink.png)


# TIPS
+ 



