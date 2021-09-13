# 解决tensorboard 1.13.1 无法打开生成的网址

使用命令：

```bash
tensorboard --logdir=logs
```

得到如下网址：

```bash
TensorBoard 1.15.0 at http://LAPTOP-10GIDQTB:6006/ (Press CTRL+C to quit)
```

出现了计算机的名字`LAPTOP-10GIDQTB`

**在命令行中加上`--host=127.0.0.1`，即可完美解决**

完整命令：

```bash
tensorboard --logdir=colab_logs --host=127.0.0.1
```

