# 常用方法&函数




- repr - 将对象转化为共解释器读取的形式

```python
>>>s = 'RUNOOB'
>>> repr(s)
"'RUNOOB'"
>>> dict = {'runoob': 'runoob.com', 'google': 'google.com'};
>>> repr(dict)
"{'google': 'google.com', 'runoob': 'runoob.com'}"
>>>
```



- translate - 根据参数table给出的表（包含256个字符）转换字符串的字符，要过滤掉的字符放到deletechars参数中

```python
1)
intab = "aeiou"
outtab = "12345"
trantab = str.maketrans(intab, outtab)   # 制作翻译表
 
str = "this is string example....wow!!!"
print (str.translate(trantab))

>>> th3s 3s str3ng 2x1mpl2....w4w!!!

2)
# 制作翻译表
bytes_tabtrans = bytes.maketrans(b'abcdefghijklmnopqrstuvwxyz', b'ABCDEFGHIJKLMNOPQRSTUVWXYZ')
 
# 转换为大写，并删除字母o
print(b'runoob'.translate(bytes_tabtrans, b'o'))
```



- fromkeys - 用于创建一个新字典，以序列seq中元素做字典的键，value为字典所有键对应的初始值

```python
seq = ('Google', 'Runoob', 'Taobao')
 
dict = dict.fromkeys(seq)
print "新字典为 : %s" %  str(dict)
 
dict = dict.fromkeys(seq, 10)
print "新字典为 : %s" %  str(dict)

>>> 新字典为 : {'Google': None, 'Taobao': None, 'Runoob': None}
>>> 新字典为 : {'Google': 10, 'Taobao': 10, 'Runoob': 10}
```



































