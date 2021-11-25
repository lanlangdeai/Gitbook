# 基础语法



【Pip】

镜像加速：

  1.临时使用

```python
pip install markdown -i https://pypi.tuna.tsinghua.edu.cn/simple
```

2.永久设置

```python
# 清华源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
# 阿里源
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
# 腾讯源
pip config set global.index-url http://mirrors.cloud.tencent.com/pypi/simple
# 豆瓣源
pip config set global.index-url http://pypi.douban.com/simple/
```

