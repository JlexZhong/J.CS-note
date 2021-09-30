---
title: 2021/9/28 课题组学习汇报（U-Net、U-Net++、BoundaryLoss）
description: 2021/9/28 向李长圣老师进行阶段学习汇报，主要内容是深度学习+CT图像处理+Abaqus单轴压缩
tags:
  - 深度学习
  - 学习汇报
categories: 学习汇报
date: 2021-09-029 18:00:09
abbrlink: 64806
---
# 2021/9/28 学习汇报总结

## U-Net

![](https://img-blog.csdnimg.cn/20181127092719427.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dpdGh1Yl8zNzk3MzYxNA==,size_16,color_FFFFFF,t_70)

- **解决什么问题？**

  - 医学图像的分割
  - 对小数据集十分友好

- **U-Net使用的方法？**

  - 整体结构就是**先编码（下采样）， 再解码（上采样）**，回归到跟原始图像一样大小的像素点的分类。
  - 继承FCN的思想，继续进行改进。但是相对于FCN，有几个改变的地方，U-Net是完全对称的，且对解码器（应该自Hinton提出编码器、解码器的概念来，即将**图像->高语义**feature map的过程看成**编码器**，**高语义->像素级别**的分类score map的过程看作**解码器**）进行了加卷积加深处理，FCN只是单纯的进行了上采样。

  - **Skip connection**：两者都用了这样的结构，虽然在现在看来这样的做法比较常见，但是对于当时，这样的结构所带来的明显好处是有目共睹的，因为可以**联合高层语义和低层的细粒度表层信息**，就很好的符合了分割对这两方面信息的需求。
  - 联合：在FCN中，Skip connection的联合是通过对应像素的求和，而U-Net则是对其的channel的concat过程。

### 效果

- **CELoss + dice_loss**，使用vgg16预训练权重；训练集：验证集 = 9：1；base_lr = 1e-4,StepLR学习率衰减器；batch_size = 2; epoch = 50。



- **Boundary Loss + Dice Loss**，权重衰减法，alpha from 1 => 0.01,使用vgg16预训练权重；训练集：验证集 = 9：1；base_lr = 1e-4,StepLR学习率衰减器；batch_size = 2; epoch = 50。

<img src="2021-09-28-zj-Research-group-report.assets/image-20210928193734174.png" alt="image-20210928193734174" style="zoom: 200%;" />

![image-20210928194652121](2021-09-28-zj-Research-group-report.assets/image-20210928194652121.png)

![image-20210928194734200](2021-09-28-zj-Research-group-report.assets/image-20210928194734200.png)

## U-Net++

![](https://img-blog.csdnimg.cn/20181127104355254.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dpdGh1Yl8zNzk3MzYxNA==,size_16,color_FFFFFF,t_70)

### 效果

![image-20210928194407791](2021-09-28-zj-Research-group-report.assets/image-20210928194407791.png)

![image-20210928194521281](2021-09-28-zj-Research-group-report.assets/image-20210928194521281.png)

![image-20210928194613551](2021-09-28-zj-Research-group-report.assets/image-20210928194613551.png)