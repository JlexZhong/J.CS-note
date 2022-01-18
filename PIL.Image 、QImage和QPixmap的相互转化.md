# PIL.Image 、QImage和QPixmap的相互转化

```python
from PIL import Image, ImageQt
from PyQt5.QtGui import QPixmap
 
image = Image.open("xxx.jpg")

# Image -> QImage
qimage = ImageQt.toqimage(image)
 
# QImage -> Image，使用这个方法
image = ImageQt.fromqimage(qimage)

# Image -> QPixmap
qpixmap = ImageQt.toqpixmap(image)
 
# QPixmap -> Image
image = ImageQt.fromqpixmap(pixmap)

# QPixmap -> QImage
qpixmap = QPixmap()
qimage = qpixmap.toImage()

# QImage -> Qpixmap
qpixmap = qimage.toPixmap()

```

