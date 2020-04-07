

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
+ 

# 核心点叙述
![](./pipeline.png)
+ 
> xx




## 消融研究
![](./ablation.png)
+ 

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



