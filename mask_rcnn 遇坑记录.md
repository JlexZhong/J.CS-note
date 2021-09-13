# mask r-cnn 遇到的坑 记录
## BUG：module 'tensorflow.compat.v2.__internal__' has no attribute 'register_clear_session_function' 已解决

更新tensorflow版本



## tensorflow.python.keras.engine' has no attribute 'Layer' 已解决

改为：

```
keras.layers.Layer
```

https://www.e-learn.cn/topic/2433086

## Tried to convert 'shape' to a tensor and failed. Error: None values not supported.

https://github.com/matterport/Mask_RCNN/issues/1820

### NO.1

You can also try call `tf.reshape(out_tensor, self.compute_output_shape(input_shape))` after each usage of Custom Layer.
More info:
https://stackoverflow.com/questions/51028861/tensorflow-compute-output-shape-not-working-for-custom-layer
[tensorflow/tensorflow#33785](https://github.com/tensorflow/tensorflow/issues/33785)

But in spite of this, the model summary differ in keras and tf.keras.

### NO.2

To solve the problem, you can change this line:
`mrcnn_bbox = KL.Reshape((s[1], num_classes, 4), name="mrcnn_bbox")(x)`
by :
`mrcnn_bbox = KL.Reshape((-1, num_classes, 4), name="mrcnn_bbox")(x)`

It works for me and the output is fine.
# tf1.13.2
##  解决编码问题：AttributeError: 'str' object has no attribute 'decode'

1. 出现问题原因：str与bytes表示的是两种数据类型，str为字符串型，bytes为字节型。对str编码encode得到bytes，
   对bytes解码得到str，两者互为转换。而上面出现问题的原因是对str字符串使用了解码，显然是猪头不对马尾。
2. 删除`decode('utf-8')`

```
pip install h5py==2.10.0
```



## invalid literal for int() with base 10: 'pths'

```python
nameinfo = "pths"
image_info.update({"id": int(name_info)})
```

强制转换成int类型时，传入的字符串必须是有数字字符组成的，例如：`x = int("111")`

## 加载权重时出现“AttributeError: ‘str‘ object has no attribute ‘decode‘ “

https://blog.csdn.net/weixin_45371989/article/details/109789132?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-3.essearch_pc_relevant&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-3.essearch_pc_relevant

### 解决办法

貌似是由于h5py模块的版本问题，改用2.10版本

```python
pip install h5py==2.10 -i https://pypi.doubanio.com/simple
```

## 发生异常: IndexError ：boolean index did not match indexed array along dimension 0; dimension is 0 but corresponding boolean dimension is 1

- 暂未解决，环境配置成一模一样也没用

- **后来发现没有更改分类的参数**T_T

## Input image dtype is bool. Interpolation is not defined with bool data type

https://stackoverflow.com/questions/62330374/input-image-dtype-is-bool-interpolation-is-not-defined-with-bool-data-type

```
pip install -U scikit-image==0.16.2
```

## Error when checking input: expected input_image_meta to have shape (15,) but got array with shape (16,)

**解决：**因为我增加了一类，但是没有修改`class_nums`

解决办法是修改NUM_CLASSES参数，增加了多少类，就对应的修改对应数值

```
NUM_CLASSES = 1 + 1  
```

https://blog.csdn.net/oMoDao1/article/details/83860101

## AttributeError: module 'yaml' has no attribute 'FullLoader'

```
pip install --ignore-installed PyYAML
```

- [1].AttributeError: 'module' object has no attribute 'FullLoader'. https://github.com/Yelp/elastalert/issues/2298

- [2].安装yaml报错：ERROR: Cannot uninstall 'PyYAML'. https://blog.csdn.net/weixin_41010198/article/details/103852838

## keras 导入包报错 ImportError: cannot import name 'moving_averages' 

```
pip3 install --upgrade --ignore-installed tensorflow-gpu==1.13.2
```

https://github.com/tensorflow/tensorflow/issues/8513

## AttributeError: module 'labelme.utils' has no attribute 'draw_label'

将版本降为3.16.2

```
pip install labelme==3.16.2
```

## IndexError: boolean index did not match indexed array along dimension 0; dimension is 0 but corresponding boolean dimension is 1

https://blog.csdn.net/Alchemist_wjt/article/details/89954791?ops_request_misc=&request_id=&biz_id=102&utm_term=IndexError:%20boolean%20index%20did%20&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-6-89954791.pc_search_result_hbase_insert&spm=1018.2226.3001.4187

新版本的labelme生成的label.png图为8位彩色图，不需要16位转8位转换！！！直接使用即可！注意观察自己的label.png的位深度！

# BUG

```bash
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-28-90029a2660a7> in <module>()
     13     ("refined_anchors_clipped", model.ancestor(pillar, "ROI/refined_anchors_clipped:0")),
     14     ("post_nms_anchor_ix", nms_node),
---> 15     ("proposals", model.keras_model.get_layer("ROI").output),
     16 ])
/content/drive/My Drive/mask rcnn_test/mrcnn/model.py in run_graph(self, images, outputs, image_metas)
   2663         outputs = OrderedDict(outputs)
   2664         for o in outputs.values():
-> 2665             assert o is not None
   2666 
   2667         # Build a Keras function to run parts of the computation graph
AssertionError: 
```

暂未找到解决方法，或许：

- 版本问题，使用的是1.13 1.15
- 是分割单类别，多类别是否会出现？
