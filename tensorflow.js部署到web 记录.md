---
title: tensorflow.js部署到web 笔记
date: 2021-09-02 12:00:09
description: tensorflow.js部署到web,部署到生产环境中，我将python训练的模型进行转换，部署到博客的网页中
tags:
  - 深度学习
  - tensorflow
  - tensorflow.js
categories: 
  - 深度学习
  - tensorflow
  - tensorflow.js
keywords:
  - 深度学习
  - tensorflow
  - tensorflow.js
---



# tensorflow.js部署到web 笔记

## BUG：

1. 无法加载源映射

   ```bash
   Could not read source map for https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest: Unexpected 404 response from https://cdn.jsdelivr.net/npm/@tensorflow/tf.min.js.map: Failed to resolve the requested file.
   ```

   解决：（https://www.nuomiphp.com/eplan/188052.html）

   ```
   换成"<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs/dist/tf.min.js"> </script>"
   ```

2. 加载模型报错 lambda，**inception_resnet_v2报错**，**inceptionV3**并不报错

   ```
   Uncaught (in promise) Error: Unknown layer: Lambda. This may be due to one of the following reasons:
   
   The layer is defined in Python, in which case it needs to be ported to TensorFlow.js or your JavaScript code.
   The custom layer is defined in JavaScript, but is not registered properly with tf.serialization.registerClass().
   at new t (errors.ts:48)
   at deserializeKerasObject (generic_utils.ts:202)
   at deserialize (serialization.ts:27)
   at i (container.ts:1329)
   at t.fromConfig (container.ts:1355)
   at deserializeKerasObject (generic_utils.ts:235)
   at deserialize (serialization.ts:27)
   at models.ts:270
   at index.ts:79
   at Object.next (index.ts:79)
   ```

   参考：

   https://github.com/tensorspace-team/tensorspace/issues/121

   https://stackoverflow.com/questions/66616597/tensorflow-js-error-in-loading-augmentation-layers-operation

   https://www.jianshu.com/p/dd2bebfa867d

   https://zhuanlan.zhihu.com/p/86355195

3. bug2在替换掉lambda后出现，基础库

   ```
   Uncaught (in promise) TypeError: undefined is not iterable (cannot read property Symbol(Symbol.iterator))
       at Fv (runtime.js:747)
       at t.fromConfig (container.js:1232)
       at eO (generic_utils.js:278)
       at aM (serialization.js:31)
       at u (container.js:1206)
       at t.fromConfig (container.js:1234)
       at eO (generic_utils.js:278)
       at aM (serialization.js:31)
       at models.js:295
       at c (runtime.js:63)
   ```

4. tf.fromPixels

   ```
   Uncaught (in promise) TypeError: tf.fromPixels is not a function
   ```

   已解决：https://stackoverflow.com/questions/55402551/why-am-i-getting-the-error-tf-frompixels-is-not-a-function

   tf.fromPixels was deprecated in version 1.0.0, use: `tf.browser.fromPixels()`

5. getImageData

   ```
   'getImageData' on 'CanvasRenderingContext2D': Value is not of type 'long'.
   ```

   我是这么写的：

   ```
   const imgData = context.getImageData(0,0,canvas.width,canvas.height);
   ```

   已解决：换成`const imgData = context.getImageData(0,0,299,299);`

6. tensorflow.js没有tf.argmax，变成了**tf.argMax**

## 加载模型时路径的写法

```
const my_model = await tf.loadLayersModel("model_js/model.json")
//正确
```

```
  const my_model = await tf.loadLayersModel("http://127.0.0.1:5502/TensorFlow%20Deployment/Course%201%20-%20TensorFlow-JS/Week%204/Examples/model_js/model.json")
//正确,前面一大串是工作区文件夹名称
```



## tensorflow.js的预测结果与tensorflow大相径庭

图片：hym_003(-)_180.jpg

### tensorflow.js

```
[[0.0038602, 0.0000056, 0.136271, 0.0231699, 4e-7, 5e-7, 1e-7, 0.0000079, 4e-7, 0.836684],]
```

### tensorflow-python

```
array([[6.1449555e-08, 7.2196451e-07, 9.9997318e-01, 2.7251541e-08,
        4.4864832e-09, 2.8673458e-07, 1.8537765e-05, 2.0686712e-06,
        9.0471025e-10, 5.0913218e-06]], dtype=float32)
```

https://github.com/tensorflow/tfjs/issues/776

后续更新部署。
