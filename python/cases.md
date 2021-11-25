# 开发实战例子



1. ### 处理特殊字符，将Unicode文本标准化

```python
import re
import unicodedata

s = 'T-shirt\xa0\xa0短袖圆领衫,\u3000体恤衫\xa0买一件\t吧'

s0 = re.sub('\xa0', ' ', s)
print(f's0: {s0}')

s1 = ''.join(c for c in s if not unicodedata.combining(c))
print(f's1: {s1}')

s2 = unicodedata.normalize('NFKC', s)
print(f's2: {s2}')

>>> s0: T-shirt  短袖圆领衫,　体恤衫 买一件	吧
>>> s1: T-shirt  短袖圆领衫,　体恤衫 买一件	吧
>>> s2: T-shirt  短袖圆领衫, 体恤衫 买一件	吧
```



2. ### 小数点精度计算

```python
from decimal import Decimal, localcontext, getcontext

a = 4.1
b = 5.329
print(a+b)  # 9.428999999999998

a1 = Decimal(str(a))
b1 = Decimal(str(b))
print(a1+b1)  # 9.429

a2 = Decimal(a)
b2 = Decimal(b)

with localcontext() as ctx:
    ctx.prec = 3
    print(a2+b2)  # 9.43

getcontext().prec = 1
print(a2+b2)  # 9


# 注意Decimal的参数必须是字符串，不能是浮点型，否则误差依旧存在。
```



3. 异常处理

```python
import sys
import traceback
import logging

logging.basicConfig(format='%(asctime)s [%(threadName)s: %(thread)d]'
                      '%(pathname)s: %(funcName)s: %(lineno)d %(levelname)s - %(message)s', level=logging.DEBUG)

def fun1():
    raise Exception("func1 throw exception")

def main():
    pass
    try:
        fun1()
    except Exception as e:
        print(e)
        traceback.print_exc(limit=2, file=sys.stdout)  # 直接输出错误信息
        logging.info(traceback.format_exc(limit=2))  # 错误信息以字符串的格式返回

        
>>>2021-07-07 16:41:40,374 [MainThread: 39204]E:/python_projects/test/except.py: main: 30 INFO - Traceback (most recent call last):
  File "E:/python_projects/test/except.py", line 20, in main
    fun1()
  File "E:/python_projects/test/except.py", line 14, in fun1
    raise Exception("func1 throw exception")
Exception: func1 throw exception 
        
```

4.耗时装饰器

```python
import time

def time_usage(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        func(*args, **kwargs)
        end = time.time()
        used = end - start
        print(f'{func.__name__} used: {used}')

    return wrapper

@time_usage
def one():
    time.sleep(3)

one()
```













