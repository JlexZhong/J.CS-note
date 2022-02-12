# 生成软件著作权程序鉴别材料-源代码word文档

## 使用pyerz生成源代码word文档

### 安装

```text
pip install pyerz
```

### 使用

#### 参数

```text
Usage: pyerz [OPTIONS]

Options:
  -t, --title TEXT            软件名称+版本号，默认为软件著作权程序鉴别材料生成器V1.0，此名称用于生成页眉
  -i, --indir PATH            源码所在文件夹，可以指定多个，默认为当前目录
  -e, --ext TEXT              源代码后缀，可以指定多个，默认为Python源代码
  -c, --comment-char TEXT     注释字符串，可以指定多个，默认为#、//
  --font-name TEXT            字体，默认为宋体
  --font-size FLOAT RANGE     字号，默认为五号，即10.5号
  --space-before FLOAT RANGE  段前间距，默认为0
  --space-after FLOAT RANGE   段后间距，默认为2.3
  --line-spacing FLOAT RANGE  行距，默认为固定值10.5
  --exclude PATH              需要排除的文件或路径，可以指定多个
  -o, --outfile PATH          输出文件（docx格式），默认为当前目录的code.docx
  -v, --verbose               打印调试信息
  --help                      Show this message and exit.
```

```bash
pyerz -i django-guardian -o django-guardian.docx
```

参考：https://zhuanlan.zhihu.com/p/339050417

目前使用pyerz生成的word文档问题较多，不能一步解决，接下来使用notepad++

## 在NotePad++中删除注释

将pyerz生成的word粘贴到**notepad++**中，打开搜索——替换：

### 单行注释：

- 查找目标为：`#.*`

- 替换为：空，即不输入
- 勾选正则表达式

![image-20220202124857350](C:\Users\26780\AppData\Roaming\Typora\typora-user-images\image-20220202124857350.png)

先查找几个试试是否正确，**有时如`#777fff`之类的颜色文本会被误删**。

### 多行注释

- 查找目标为：`""".*?\"""`以及`'''.*?'''`

- 替换为：空，即不输入
- 勾选正则表达式

![image-20220202130740961](C:\Users\26780\AppData\Roaming\Typora\typora-user-images\image-20220202130740961.png)

### 空行

- 删除空行，操作方法为：编辑->行操作->移除空行(包括空白字符)
- 删除行尾空格，操作方法为：编辑->空白字符操作->移除行尾空格
- Tab 转空格，操作方法为：编辑->空白字符操作->TAB 转空格

参考：https://blog.csdn.net/wah8868/article/details/82907427

**注意：**

- **还需对word中的长行进行处理。**
- 中文字体：宋体；西文字体：Times new roman
- 字体大小：小四
- 行间距：固定值：14磅

