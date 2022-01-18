# PyQt如何找到组件的子控件；findChild()

使用`findChild()`的方法，需要传入两个参数：

- type:  比如你要找QLabel，就写`QtWidgets.QLabel`
- name: 要找的组件的名字，通过`setObjectName()`的名字

如：我要找QFrame里面的名字叫"title_label"的label，那么：

```python
from pyqt5 import QtWidgets

titleLabel = qframe.findChild(QtWidgets.QLabel,"title_label")
```

