# python绘制三维点云图

x：（1,2,3,4,4,5，.....）

## matplotlib

```python
import matplotlib.pyplot as plt
import numpy as np
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(20,20))
ax = Axes3D(fig)

# x
x = np.load(r"E:\\My Projects\\rocks_view\\x.npy")
# y
y = np.load(r"E:\\My Projects\\rocks_view\\y.npy")
# z
z = np.load(r"E:\\My Projects\\rocks_view\\z.npy")

#ax.plot3D(x,y,z)
ax.scatter3D(x,y,z,s=100)
plt.show()
```

![image-20220117151544148](C:\Users\26780\AppData\Roaming\Typora\typora-user-images\image-20220117151544148.png)

## mayavi

```python
import numpy as np
from mayavi import mlab
# x
x = np.load(r"E:\\My Projects\\rocks_view\\x.npy")
# y
y = np.load(r"E:\\My Projects\\rocks_view\\y.npy")
# z
z = np.load(r"E:\\My Projects\\rocks_view\\z.npy")

#对该数据进行三维可视化
s = mlab.points3d(x,y,z)
mlab.show()

```

![image-20220117151700182](C:\Users\26780\AppData\Roaming\Typora\typora-user-images\image-20220117151700182.png)

## PyqtGraph

```python
# -*- coding: utf-8 -*-
"""
Demonstrates use of GLScatterPlotItem with rapidly-updating plots.

"""

## Add path to library (just for examples; you do not need this)

from pyqtgraph.Qt import QtCore, QtGui
import pyqtgraph.opengl as gl
import numpy as np

app = QtGui.QApplication([])
w = gl.GLViewWidget()
# w.opts['distance'] = 20

w.setWindowTitle('pyqtgraph example: GLScatterPlotItem')

g = gl.GLGridItem()
w.addItem(g)

# x
x = np.load(r"E:\\My Projects\\rocks_view\\x.npy")
# y
y = np.load(r"E:\\My Projects\\rocks_view\\y.npy")
# z
z = np.load(r"E:\\My Projects\\rocks_view\\z.npy")
pos = np.empty((len(x),3))
for i in range(len(x)):
    pos[i] = (x[i],y[i],z[i])

pos = np.array(pos)
sp1 = gl.GLScatterPlotItem(pos=pos,size=0.4, pxMode=False)
w.addItem(sp1)

w.setCameraPosition()


w.show()


## Start Qt event loop unless running in interactive mode.
if __name__ == '__main__':
    import sys
    if (sys.flags.interactive != 1) or not hasattr(QtCore, 'PYQT_VERSION'):
        QtGui.QApplication.instance().exec_()

```

![image-20220117151809143](C:\Users\26780\AppData\Roaming\Typora\typora-user-images\image-20220117151809143.png)