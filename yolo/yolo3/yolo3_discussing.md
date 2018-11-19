
# YOLO V2 论文阅读总结和讨论

look for [papers for yolo3](https://github.com/leoluopy/paper_discussing/blob/master/yolo/yolo3/YOLOv3.pdf)
contributer : [leoluopy](https://github.com/leoluopy)

+ 如果分享内容对你有帮助和启发，欢迎start / fork / follow 谢谢 ^_^ !
+ 由于知识有限，内容有错误，欢迎请提issue 谢谢 ^_^!
+ 如果对内容有疑问，欢迎提issue 谢谢 ^_^!
+ 如果你最近也有读深度学习相关paper ， 能认识更多志同道合朋友，还不加入分享 ？？   ^_^! 联系微信：leoluopy

# Overview

+ 相对于yolov2，提出了darknet53，并增加更多passthrough layer ， 体积更大，但是更精准。
+ 在 320 × 320 分辨率下，YOLOv3 每帧 22 ms 并达到 28.2 mAP,和相同分辨率SSD一样精准，但是快3倍。

![](./compare.png)
![](./yolo3_effe.png)


## 与YOLOV2 对比清单

+ ![](./predict_tensor.PNG)
+ 使用相同的 BoundingBox 预测tensor , 并且每一个box仅预测一个object
+ 
