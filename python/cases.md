# 开发实战例子



1. 处理特殊字符，将Unicode文本标准化

```
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



2. 小数点精度计算

```
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












