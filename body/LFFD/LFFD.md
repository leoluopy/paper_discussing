

# LFFD 核心点笔记

looking for papers for [LFFD](https://arxiv.org/abs/1904.10633)

contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.欢迎watch ，star.
+ 微信号：leoluopy，如有疑问，欢迎交流，拍砖

<img width="200" height="200" src="https://github.com/leoluopy/paper_discussing/blob/master/wechat_id.jpeg"/>


# Overview
+ 在检测领域中，基于anchor的方法，目前来看是主流方案，本文新颖的提出了anchor free 的方案，并且在人脸检测的子领域
中取得了非常不错的效果，在类比精确的人脸检测算法的情况下，牺牲了极少的精度，换取了非常大的速率提升。
+ 本文实现anchor free 的检测方案重新定义了backBone特征提取结构
+ 在重新设计网络之前，本文重新梳理了感受野相关理念和理解。

# 效果描述
+ ![](./ret_FDDB.png)
+ 上图是在FDDB数据集上的ROC曲线结果
+ 连续和非连续的解释 
    + 定好一个阈值之后，根据超过此阈值定和低于此阈值，就可以得出混淆矩阵，
    + 对于每个混淆矩阵，我们计算两个指标TPR和FPR,以FPR为x轴，TPR为y轴画图，就得到了ROC曲线
    + 这种定好阈值，单个混淆矩阵画ROC曲线称之为非连续ROC曲线
    + 如果在上述模型中我们没有定好阈值，而是将模型预测结果从高到低排序，将每次概率值依次作为阈值，那么就可以得到多个混淆矩阵。
    + 这种多个阈值，多个混淆矩阵相叠加得到的ROC曲线，称之为连续ROC曲线
> 连续ROC曲线因为有取到更低的阈值，往往更加严格，得分更低。
+ ![](./ret_WIDERFACE.png)
+ 在WIDER FACE 中的结果，分为多个子数据集的对比
+ ![](./ret_runEffe.png)
+ 运行效率对比，比S3FD快大约３倍，比DSFD快大约10倍。

# 核心点叙述
+ ![](./erf.png)
+ 在实际图像中，感受野就是自然存在的anchor,本文通过重新设计backBone的方法，设计了感受野的大小，从而达到了和anchor
类似的相关，从而实现了anchor free 的效果
    + 对于极小人脸，感受野除了需要包含人脸同时，还需要包含比较多的场景信息，例如，人脸已经看不清的脸，但是可以通过肩膀判断出这是人脸
    + 对于中等大小人脸，感受野除了需要包含人脸同时，需要少部分场景信息。
    + 对于很大人脸，由于脸部信息丰富，只需要脸部信息。
+ ![](./RF_distribute.png)
+ Location对应下图中网络位置
+ RF size: 感受野大小
+ RF stride: 如果把感受野类比为在原图中的预选框滑动，这个stride就是每次滑动的像素
+ Continuous face scale: 被感受野捕获的人脸大小。
> 例如c8的　RF size: 55 , featureMapSize: 159 ,也就是有 159x159个感受野用于预测人脸。每个人脸在实际图片上滑动距离是4像素

+ ![](./RF_compute.png)
+ 感受野计算方法规律
    + 初始感受野大小 1x1
    + 感受野大小经过卷积后增大，增大速率与累积stride成正比

# 模型结构叙述
+ ![](./structure.png)
+ 对于模型的设计十分简洁，没有特殊的卷积或者池化操作
+ 图中各个箭头代表不同的pading和stride.加号是对层结果进行累加（是常见的残差处理）
+ Loss branch也分为两部分，一部分是人脸分类loss,一部分是box坐标loss

# 训练及Loss设计
+ ![](./loss.png)
+ 上图是模型回归结果的 GT定义。
> 和基于 anchor 方法回归偏移量和指数参数，不同的是本文方法直接回归了人脸框和感受野的相对关系。
+ RFx 是感受野中心的x坐标,RFy 是感受野中心的y坐标（每个感受野都有他对应的在原图中的位置，是图像中自然存在的anchor）
+ RFs 是感受野大小
+ 其他训练细节
    + 人脸大小在预选大小【0.9-1],[1-1.1]之间人脸被忽略
    + 同时两个人脸落到感受野中心的，这个感受野被忽略不计loss
    + softmax-crossEntropy为分类loss,被标记为人脸时激活，其他时候抑制。
    + 激活时，BoxLoss有L2正则化
    + 负样本的感受野总比正样本多很多，将负样本感受野Loss排序，只反向传播最大的。
    + 预处理（x-127.0）/127.5
    + 优化器SGD 0.9 ,不进行weight decay , batch-size: 32 .模型很小所以不用　weight-decay
    + 初始学习率0.1, 总共150万. 迭代衰减学习率x0.1。衰减位置是： 60万，100万, 120万 , 140万
    + 两张1080Ti训练5天。 

# TIPS
+ ![](./FLOPS.png)
+ 上图是各个模型的，模型参数，模型FLOPS，和模型大小，FLOPS 的定义代表了神经网络模型计算的复杂度，但并不一定是线性关系。
因此本文提出了Enet这个标准表征了模型的运算效率，Enet越大，模型运算效率越高(单位时间能运算的FLOPS数量)
+ ![](./EnetFlops.png)



