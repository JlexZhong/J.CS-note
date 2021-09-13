# HTML 学习笔记

## &lt;li&gt;

定义列表。

"<ol>"：有序列表；

"<ul>"：无序列表。

## &lt;a&gt;

定义超链接

## id,name,class的理解

- id、name、class属性是什么？
  - id是html页面中元素的唯一标示，属性值在页面中不能重复，每个元素的id不同，可以设置也可以不设置；
  - name属性值可以重复，指的是标签的名称；
  - class可简单的理解为类属性，属性值在页面中不唯一；

- id、name、class的用途
  - id是标签的唯一标识，多用于**js脚本**中，比如页面中有多个元素，让我们想在js脚本中对某个特定元素进行设置的时候，我们可以根据id来直接访问该元素。
  同时，id也可用于**css样式**中，当我们想对某个单独的元素做出改变样式时候可以进行设置，使用  `#元素id{ }` 方式来改变样式
  - name多用于**表单**中，用来和服务器进行交互，如CheckBox标签和radio标签等，对应的name属性的值就是提交表单后变量的名称。

  - class多用于设置**CSS样式** ，当我们想让很多元素拥有相同的样式时，可以通过class属性的值来统一选择，通常为 `.class的属性{} ` 设置css样式做法一般是先通过类设置大部分相同的元素样式，再通过ID设置独特的元素样式。

## &lt;a&gt;中的 target="_blank"属性

- _blank – 在新窗口中打开链接
- _parent – 在父窗体中打开链接
- _self – 在当前窗体打开链接,此为**默认值**
- _top – 在当前窗体打开链接，并替换当前的整个窗体(框架页)
- 一个对应的框架页的名称 – 在对应框架页中打开



## data-aoc

```
<div data-aos="fade-up">
```

平滑上升效果

## <u>BUG</u>：Uncaught ReferenceError: $ is not defined

使用CDN地址引用jQuery

```
    <script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>

```

## HTML中返回上级目录的写法

当前目录：`https://jlexzhong.github.io/blog/`

返回上级应该为：`href="../index.html"`

https://www.cnblogs.com/kenshinobiy/p/7783135.html

