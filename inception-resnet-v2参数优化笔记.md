# inception-resnet-v2优化笔记

## csdn数据集

### 1

```
    image_size = 299
    batch_size = 32
    num_train = 250
    num_val = 50
    epochs = 30
	model.compile(loss=tf.keras.losses.CategoricalCrossentropy(from_logits=False),  # BUG：交叉熵损失函数
                      optimizer=tf.keras.optimizers.Adam(lr=0.001, beta_1=0.9, beta_2=0.999),  
                      metrics=['accuracy'])
    x = layers.Dropout(0.5)(x)
```

![2021-08-20-i and r 2 loss](C:\Users\26780\OneDrive - ecut.edu.cn\图片\深度学习\2021-08-20-i and r 2 loss.png)![2021-08-20-i and r 2 acc](C:\Users\26780\OneDrive - ecut.edu.cn\图片\深度学习\2021-08-20-i and r 2 acc.png)

### 2

在1的基础上

```
x = layers.Dropout(0.4)(x)
reduce_lr =  tf.keras.callbacks.ReduceLROnPlateau(monitor='val_loss', patience=15,  verbose=1,mode='auto')
```

![动态调整lr，adam-los](C:/Users/26780/OneDrive - ecut.edu.cn/图片/深度学习/动态调整lr，adam-los.png)![动态调整lr，adam-acc](C:/Users/26780/OneDrive - ecut.edu.cn/图片/深度学习/动态调整lr，adam-acc.png)

### 3

```
x = layers.Dropout(0.3)(x)
lr=0.001, decay=0.0002, momentum=0.9
sgd = SGD(lr=lr, decay=decay, momentum=momentum, nesterov=True)
print('================编译模型=================')
        
model.compile(loss=tf.keras.losses.CategoricalCrossentropy(from_logits=False),  # BUG：交叉熵损失函数
        optimizer=sgd,  #tf.keras.optimizers.Adam(lr=0.001, beta_1=0.9, beta_2=0.999)
        metrics=['accuracy'])
# 动态更改学习率
reduce_lr =  tf.keras.callbacks.ReduceLROnPlateau()
        
```

![08-20-i r sgd -loss](C:/Users/26780/OneDrive - ecut.edu.cn/图片/深度学习/08-20-i r sgd -loss.png)![08-20-i r sgd -acc](C:/Users/26780/OneDrive - ecut.edu.cn/图片/深度学习/08-20-i r sgd -acc.png)

## scidbk镜下矿物薄片图像数据集

### 1

```python
总计：989
train:796
val:147
test:46

lr=0.001, decay=0.0002, momentum=0.9
sgd = SGD(lr=lr, decay=decay, momentum=momentum, nesterov=True)
reduce_lr =  tf.keras.callbacks.ReduceLROnPlateau()
x = layers.Dropout(0.4)(x)
```

```

24/24 [==============================] - 374s 14s/step - loss: 2.1553 - accuracy: 0.4824 - val_loss: 0.7156 - val_accuracy: 0.7823
Epoch 2/30
24/24 [==============================] - 352s 14s/step - loss: 0.7679 - accuracy: 0.7475 - val_loss: 0.3818 - val_accuracy: 0.8503
Epoch 3/30
24/24 [==============================] - 290s 12s/step - loss: 0.4792 - accuracy: 0.8354 - val_loss: 0.3833 - val_accuracy: 0.8503
Epoch 4/30
24/24 [==============================] - 280s 11s/step - loss: 0.3891 - accuracy: 0.8693 - val_loss: 0.2691 - val_accuracy: 0.9048
Epoch 5/30
24/24 [==============================] - 331s 13s/step - loss: 0.2923 - accuracy: 0.8995 - val_loss: 0.2480 - val_accuracy: 0.8980
Epoch 6/30
24/24 [==============================] - 371s 15s/step - loss: 0.2635 - accuracy: 0.9133 - val_loss: 0.1679 - val_accuracy: 0.9388
Epoch 7/30
24/24 [==============================] - 374s 15s/step - loss: 0.3156 - accuracy: 0.8869 - val_loss: 0.1656 - val_accuracy: 0.9524
Epoch 8/30
24/24 [==============================] - 355s 14s/step - loss: 0.2576 - accuracy: 0.9146 - val_loss: 0.2341 - val_accuracy: 0.9116
Epoch 9/30
24/24 [==============================] - 365s 15s/step - loss: 0.2239 - accuracy: 0.9347 - val_loss: 0.1897 - val_accuracy: 0.9252
Epoch 10/30
24/24 [==============================] - 320s 13s/step - loss: 0.2377 - accuracy: 0.9196 - val_loss: 0.1559 - val_accuracy: 0.9456
Epoch 11/30
24/24 [==============================] - 289s 12s/step - loss: 0.2157 - accuracy: 0.9108 - val_loss: 0.1439 - val_accuracy: 0.9524
Epoch 12/30
24/24 [==============================] - 288s 12s/step - loss: 0.1980 - accuracy: 0.9296 - val_loss: 0.1760 - val_accuracy: 0.9320
Epoch 13/30
24/24 [==============================] - 288s 12s/step - loss: 0.1712 - accuracy: 0.9472 - val_loss: 0.1125 - val_accuracy: 0.9728
Epoch 14/30
24/24 [==============================] - 289s 12s/step - loss: 0.2244 - accuracy: 0.9246 - val_loss: 0.1753 - val_accuracy: 0.9252
Epoch 15/30
24/24 [==============================] - 290s 12s/step - loss: 0.2167 - accuracy: 0.9309 - val_loss: 0.1282 - val_accuracy: 0.9524
Epoch 16/30
24/24 [==============================] - 292s 12s/step - loss: 0.1749 - accuracy: 0.9372 - val_loss: 0.1213 - val_accuracy: 0.9456
Epoch 17/30
24/24 [==============================] - 300s 12s/step - loss: 0.2063 - accuracy: 0.9234 - val_loss: 0.1781 - val_accuracy: 0.9456
Epoch 18/30
24/24 [==============================] - 364s 15s/step - loss: 0.1768 - accuracy: 0.9397 - val_loss: 0.1639 - val_accuracy: 0.9456
Epoch 19/30
24/24 [==============================] - 357s 14s/step - loss: 0.1618 - accuracy: 0.9460 - val_loss: 0.1257 - val_accuracy: 0.9592
Epoch 20/30
24/24 [==============================] - 553s 22s/step - loss: 0.1960 - accuracy: 0.9422 - val_loss: 0.1187 - val_accuracy: 0.9524
Epoch 21/30
24/24 [==============================] - 355s 14s/step - loss: 0.1456 - accuracy: 0.9510 - val_loss: 0.1159 - val_accuracy: 0.9524
Epoch 22/30
24/24 [==============================] - 382s 15s/step - loss: 0.1256 - accuracy: 0.9523 - val_loss: 0.0699 - val_accuracy: 0.9660
Epoch 23/30
24/24 [==============================] - 356s 14s/step - loss: 0.1445 - accuracy: 0.9523 - val_loss: 0.0798 - val_accuracy: 0.9864
Epoch 24/30
24/24 [==============================] - 377s 15s/step - loss: 0.1284 - accuracy: 0.9422 - val_loss: 0.1049 - val_accuracy: 0.9592
Epoch 25/30
24/24 [==============================] - 344s 14s/step - loss: 0.1593 - accuracy: 0.9384 - val_loss: 0.1042 - val_accuracy: 0.9728
Epoch 26/30
24/24 [==============================] - 380s 15s/step - loss: 0.1241 - accuracy: 0.9598 - val_loss: 0.1363 - val_accuracy: 0.9592
Epoch 27/30
24/24 [==============================] - 367s 15s/step - loss: 0.1538 - accuracy: 0.9460 - val_loss: 0.1196 - val_accuracy: 0.9660
Epoch 28/30
24/24 [==============================] - 378s 15s/step - loss: 0.0946 - accuracy: 0.9636 - val_loss: 0.0695 - val_accuracy: 0.9592
Epoch 29/30
24/24 [==============================] - 366s 15s/step - loss: 0.1100 - accuracy: 0.9648 - val_loss: 0.1312 - val_accuracy: 0.9456
Epoch 30/30
24/24 [==============================] - 368s 14s/step - loss: 0.1270 - accuracy: 0.9560 - val_loss: 0.0658 - val_accuracy: 0.9660
```

![sci_drop0.4_sgd0.001 -loss](C:/Users/26780/OneDrive - ecut.edu.cn/图片/深度学习/sci_drop0.4_sgd0.001 -loss.png)

![sci_drop0.4_sgd0.001 -acc](C:/Users/26780/OneDrive - ecut.edu.cn/图片/深度学习/sci_drop0.4_sgd0.001 -acc.png)

