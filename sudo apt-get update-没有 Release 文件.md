# sudo apt-get update提示E: 仓库 “http://mirrors.aliyun.com/ubuntu eoan Release” 没有 Release 文件。 解决办法

https://www.cnblogs.com/sunanli/p/13797042.html

18.04.3的ubuntu
sudo apt-get install python2.7.的时候系统提示，
sudo apt-get update的指令同样是如此
换了19.10版本还是有相同的错误提示，说明这个不是版本的问题，是源配置错误的问题，
sources.list配置有误

忽略:1 http://mirrors.aliyun.com/ubuntu eoan InRelease
忽略:2 http://mirrors.aliyun.com/ubuntu eoan-updates InRelease
忽略:3 http://mirrors.aliyun.com/ubuntu eoan-backports InRelease
忽略:4 http://mirrors.aliyun.com/ubuntu eoan-security InRelease
错误:5 http://mirrors.aliyun.com/ubuntu eoan Release
SECURITY: URL redirect target contains control characters, rejecting. [IP: 117.27.140.186 80]
错误:6 http://mirrors.aliyun.com/ubuntu eoan-updates Release
SECURITY: URL redirect target contains control characters, rejecting. [IP: 117.27.140.186 80]
错误:7 http://mirrors.aliyun.com/ubuntu eoan-backports Release
SECURITY: URL redirect target contains control characters, rejecting. [IP: 117.27.140.186 80]
错误:8 http://mirrors.aliyun.com/ubuntu eoan-security Release
SECURITY: URL redirect target contains control characters, rejecting. [IP: 117.27.140.186 80]
正在读取软件包列表… 完成
E: 仓库 “http://mirrors.aliyun.com/ubuntu eoan Release” 没有 Release 文件。
N: 无法安全地用该源进行更新，所以默认禁用该源。
N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节。
E: 仓库 “http://mirrors.aliyun.com/ubuntu eoan-updates Release” 没有 Release 文件。
N: 无法安全地用该源进行更新，所以默认禁用该源。
N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节。
E: 仓库 “http://mirrors.aliyun.com/ubuntu eoan-backports Release” 没有 Release 文件。
N: 无法安全地用该源进行更新，所以默认禁用该源。
N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节。
E: 仓库 “http://mirrors.aliyun.com/ubuntu eoan-security Release” 没有 Release 文件。
N: 无法安全地用该源进行更新，所以默认禁用该源。
N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节。

解决方法：
1.在官网源https://mirrors.ustc.edu.cn/repogen/下载对应版本最新的源，比如我是19.10版本的ubuntu，对应下载的是这个
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191030091415205.png)
2.下载sources.list完成之后将源拷贝到对应的位置将原文件覆盖

```python
sudo cp sources.list /etc/apt
```

- 1

再执行sudo apt-get
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191030091855226.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2poX2x1Y2hp,size_16,color_FFFFFF,t_70)