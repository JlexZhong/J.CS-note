# python os.listdir() 排序问题

```python
import os
 
 
''' 获取 文件夹名 列表 '''
file_list = os.listdir("XXXXXXX")
 
 
''' 文件夹名 排序 '''
# 文件夹名 按字符串排序
file_list.sort()
print(file_list)
# ['file1', 'file101', 'file102', 'file103', 'file11', 'file12',
# 'file13', 'file2', 'file21', 'file22', 'file23', 'file3']
 
# 文件夹名 按数字排序
file_list.sort(key=lambda x: int(x[4:]))
print(file_list)
# ['file1', 'file2', 'file3', 'file11', 'file12', 'file13',
# 'file21', 'file22', 'file23', 'file101', 'file102', 'file103']
```

