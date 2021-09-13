# Python批量删除含有指定字符的文件或文件夹

```python
# encoding: UTF-8

import os
from pathlib import Path

p = Path(r'./test/erli')
# 这里不得不感慨，Python的库，几乎满足你所有需要，看，连这个递归查找过滤都有了！
# 实现思路：递归遍历文件夹中的文件，如果文件名包含"(-)"，就删掉，下面是代码：
for file in p.rglob('*(-)*'):    
    if os.path.isfile(file):      #这里判断下，如果是文件夹就先不删
        os.remove(file)
```

参考：

https://www.jianshu.com/p/17ae57c19d1d

