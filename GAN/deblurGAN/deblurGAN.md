

# deblurGAN 论文阅读总结和讨论

look for [papers for deblurGAN](./ECCV2018_deblurGAN.pdf)
contributer : [leoluopy](https://github.com/leoluopy)

+ 欢迎提issue.欢迎watch ，star.
+ 微信号：leoluopy
+ 关注AI前沿技术及商业落地，欢迎交流

<img width="200" height="200" src="https://github.com/leoluopy/paper_discussing/blob/master/wechat_id.jpeg"/>


# Overview
+ 端到端的条件GAN修复网络
+ 在PSNR和SSIM参数对比情况下比同期deepblur快5倍
+ 提出新颖的模糊方法和新的使用检测网络评价优劣的手段

> a method generating synthetic motion blurred image GANs preserve texture details , create image manifold and look perceptually convincing

>  loss design and new architecture 5x faster than deep blur(the fastest before 2018)

## 性能对比
![](./compare_PSNR_SSIM.png)
> PSNR 用于评价画面质量，品质指数

> SSIM 用于评价图像结构相似性指数

> 速率方面，由于舍弃了大量的残差堆叠过程，速率指数级别提升。

![](./output.png)

## 结构综述
![](./network.png)
+ 

## GAN 提要
![](./GAN_loss_ori.png)

![](./W-distance.png)

![](./WGAN-loss.png)

![](./WGAN-GP.png)

> 先讲GAN的必要性？

+ 

## loss 方法
![](./deblurGAN-loss.png)

![](./deblurGAN-GAN-loss.PNG)

![](./deblurGAN-content-loss.png)



## Training 方法
![](./training_sketch_map.PNG)



## 在目标检测中的贡献
![](./detection-contribute.png)

![](./detection-contribute2.png)
 




