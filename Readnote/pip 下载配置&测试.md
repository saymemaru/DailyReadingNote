
``pip install --proxy http://127.0.0.1:7897 httpx``
>强制设置代理测试下载小包

``curl -x http://127.0.0.1:7897 http://www.google.com``
>测试代理服务器

``curl -x http://127.0.0.1:7897 https://pypi.org/simple/``
>测试下载源

``pip config list``
>查看所有配置文件位置

```ini
[global]
proxy = http://127.0.0.1:7897
index-url = https://pypi.org/simple
trusted-host = pypi.org pypi.python.org files.pythonhosted.org
```

>修改pip.ini文件的 proxy和 trusted-host