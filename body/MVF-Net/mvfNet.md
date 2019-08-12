

# MVF-Net 核心点解析

looking for papers for [MVF-Net](https://arxiv.org/abs/1904.04473)

contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.欢迎watch ，star.
+ 微信号：leoluopy，如有疑问，欢迎交流，得文时浅，或有纰漏，请不吝指教。

<img width="200" height="200" src="https://github.com/leoluopy/paper_discussing/blob/master/wechat_id.jpeg"/>


# Overview
+ 人脸三维建模是一个长期研究的课题，人脸三维数据稀少，并采集成本高，人脸三维重建的监督学习发展遇到不小瓶颈，
本文提出了一个人脸三维重建的半监督学习方法，并超越了不少同时期其他state-of-art方法。

![](./result.png)
![](./metricError.png)
> 在数据集MICC上和其他方法的对比，均有不同程度的提升。
![](./compare.png)
> 实现效果的另一侧面说明，由此也可以发现实现最终精度误差大约在1cm左右。


# 方法叙述
+ ![](./core_idea.png)
+  
+ ![](./model_struct.png)
+ 
+ ![](./project_parameter.png)
+
+ ![](./3dmm_equation.png) 

# 训练方法
+ 

# 投影描述和Loss设计

+ ![](./project_equation.png)
+ ![](./prjection_AB.png)
+ ![](./prjectionAB2.png)

## 监督训练Loss
+ ![](./superviseLoss.png)

## 无监督训练Loss
+ ![](./photoLoss.png)
+
+ ![](./flowLoss.png)
+
+ ![](./unsuperviseLoss.png)





