**BUG：**

- ```
  BUG:QObject::startTimer: Timers cannot be started from another thread
  ```

- 原因：多线程问题。在子线程中对主线程的对象进行操作。

- 解决方案：子线程中发送信号，然后再主线程中接受信号并执行相应的操作。

**BUG：**

- ```
  QObject::setParent: Cannot set parent, new parent is in a different thread
  QBackingStore::endPaint() called with active painter; did you forget to destroy it or call QPainter::end() on it?
  ```

- 解决方法：子线程发送信号，数据为item，报错！！

- 暂未解决

BUG：

+ ```
  ImportError: cannot import name ‘Flask’ from partially initialized module ‘flask’ (most likely due to a circular import) (C:\Users
  \Administrator\PycharmProjects\test\venv\lib\site-packages\flask_init_.py)
  
  ```

+ 原因：导入的包和运行.py脚本的名字相同，改名即可

