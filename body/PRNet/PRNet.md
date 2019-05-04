

# PRNet 论文阅读总结和讨论

look for [papers for PRNet](https://arxiv.org/pdf/1803.07835.pdf)
contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.欢迎watch ，star.
+ 微信号：leoluopy
+ 关注AI前沿技术及商业落地，欢迎交流

<img width="200" height="200" src="https://github.com/leoluopy/paper_discussing/blob/master/wechat_id.jpeg"/>


# Overview
![](./prnet_overview.gif)
+ 端到端的人脸3D重建模型，同时直接预测人脸的【实际上就是UV空间预测并直接解码，UV空间后面叙述】
> 以前的模型或者需要首先回归3DMM参数来计算3D空间，或者需要回归特征3D点随后进行非线性优化获取3DMM参数，随后使用3DMM参数来得到稠密的人脸模型,这些方法都是基于3DMM模型的。
> 当然也有2D的方法，先回归得到2D的不少坐标点，并预测深度图，根据深度度和2D点重建稠密3D人脸
+ 这个模型做到了在1080的显卡上仅仅需要 9ms的速率，相对于之前的各种方法有了很明显的提升，同时在评判指标CED，NME上也有显著的提升
> NME : normalised mean error : 归一化的，参考长度的坐标偏差衡量指标，用来评判人脸关键点回归质量的重要指数

> CED : NME和数据集比例曲线，衡量在NME达到一定错误率时，已经覆盖的数据集比例，模型的鲁棒性指标

# 效果概览
![](./effect.png)
+ 人脸关键点和3D重建结构效果

![](./change_face.png)
+ PRNet 根据人脸关键3D位置及其相应纹理，进行的换脸术。

![](./mesh_ret2.png)
+ PRNet重建的稠密3D人脸

# UV 空间
![](./UV_space.png)


# 网络结构
![](./net_structure.png)


# Loss设计
![](./net_mask.png)
![](./loss.png)


# 训练细节



# 测试结果
![](./face_alignment_ret.png)
![](./face_alignment_coor_ret.png)
+

![](./face_alignment_table.png)
+

![](./face_reconstruction_ret.png)
+

![](./mesh_ret.png)
+

![](./compare_with_gt.png)
+











