# py-valid-proxy

## В работе

### Installation

```
pip install py-valid-proxy
```

### Usage

``` python
from py_valid_proxy import valid_proxy

"""Valid proxy server ('alive' or 'dead')

Parameters
----------
host : str
    IP Address
port : int
    Port
scheme: str, optional
    Scheme (default is 'http')
timeout: int, optional
    Connect timeout is number of seconds (default is 5 sec.)
Returns
-------
    None if proxy is 'dead'
    dict if proxy is 'alive'
    {
        "scheme": str, # http, https
        "host": str,
        "port": int,
        "export_address": list[str],
        "anonymity": str, # transparent, anonymous, high_anonymous # noqa
        "country": str # ISO Code 
        "response_time": float
    }
"""
proxy_info = valid_proxy('8.219.97.248', 80, 'https', 10)
if proxy_info:
	print('is alive')
else:
	print('is dead')
```

```shell
$ poetry run valid_proxy https://50.207.199.85:80 -l
Host: 50.207.199.85
Port: 80
Scheme: https
Response time: 0.51
Export address: []
Anonymity: transparent
Country : US
https://50.207.199.85:80 ... alive

$ poetry run valid_proxy http://50.207.199.85:80 -l
INFO:py_valid_proxy.main: HTTPConnectionPool(host='50.207.199.85', port=80): Max retries exceeded with url: http://httpbin.org/get?show_env=1&cur=1700497583.799429 (Caused by ProxyError('Unable to connect to proxy', ConnectTimeoutError(<urllib3.connection.HTTPConnection object at 0x7f1219ed0750>, 'Connection to 50.207.199.85 timed out. (connect timeout=5)')))
http://50.207.199.85:80 ... is dead
```