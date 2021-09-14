---
title: 使用Mask-R-CNN训练自己的数据集
date: 2021-09-09 12:00:09
description: 如何使用Mask R-CNN训练自己的数据集，以及遇到的use_multiprocessing=True的BUG 
tags:
  - Mask R-CNN
  - 深度学习
  - tensorflow
  - keras
  - 实例分割
categories: 
  - Mask R-CNN
  - tensorflow
  - 实例分割
keywords:
  - Mask R-CNN
  - 深度学习
  - tensorflow
  - keras
  - 实例分割

---

# 使用Mask-R-CNN训练自己的数据集

训练自己数据的步骤：

## 安装Labelme

```
pip install labelme
```

```
pip install pyqt5
```

```
pip install pillow==4.0.0
```

## 标注数据

1. 使用labelme得到json标注文件

2. 使用命令labelme_json_to_dataset 1.json得到json文件夹

3. 也可以用批处理脚本得到所有json文件夹

4. 得到4个文件夹标注信息


## 代码中需要改动的地方：

- NUM_CLASSES：表示类别的个数

- self.add_class("shapes", 1, "category1") 添加标签中定义的类别

- 指定好路径


```python
dataset_root_path="mydata/"

img_floder = dataset_root_path + "pic"

mask_floder = dataset_root_path + "cv2_mask"

imglist = os.listdir(img_floder)

count = len(imglist)
```

- DETECTION_MIN_CONFIDENCE 指定的稍微小一点可以得到更多结果


## 训练之后测试结果

- 先得到.h5的模型文件

- 参考demo.ipynb文件来写测试脚本

# Using a generator with `use_multiprocessing=True` and multiple workers may duplicate your data. Plea

https://github.com/keras-team/keras/pull/8662

https://github.com/matterport/Mask_RCNN/issues/514

https://github.com/matterport/Mask_RCNN/pull/740

https://blog.csdn.net/qq_35874169/article/details/116203228

https://www.gitmemory.com/issue/reigngt09/mask-rcnn/2/623180746

退出重新启动Google colab运行时即可解决问题。