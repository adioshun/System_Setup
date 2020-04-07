# Proxy 설정 

## 1. 글로벌 

```
#bashrc
export http_proxy="http://168.219.61.xxx:8080"
export https_proxy="http://168.219.61.xxx:8080"
export no_proxy="127.0.0.1, localhost, 168.219.61.*"

#unset http_proxy
#unset https_proxy
```


## 2. apt
```
#sudo vi /etc/apt/apt.conf.d/90proxy  #90숫자는 큰 의미 없음, 중복 되지 않는 숫자로 지정 
Acquire {
  HTTP {
    Proxy "http://168.219.61.xxx:8080";
  };
  HTTPS {
    Proxy "https://168.219.61.xxx:8080";
  };
}
```
```
# 키서버 추가 : 
$ sudo apt-key adv --keyserver-options http-proxy=http://168.219.61.252:8080/ --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
$ sudo -E add-apt-repository {ppa:alexx2000/doublecmd}
```

## 3. pip 
```
$ pip install --proxy http://proxy.252:port 패키지명 
$ python -m pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org [패키지명]

# vi ~/.pip/pip.conf 
[global]
trusted-host = pypi.org files.pythonhosted.org
```


## conda

```python
$ conda config --set ssl_verify false
$ vi ~/.condarc

"""
ssl_verify: false
proxy_servers:
 http: http://168.219.61.252:8080
 https: http://168.219.61.252:8080
#앞 공백은 스페이스로, tab아님 
"""
```
## Docker

```python 
# Docker 버전 17.07 이상
$ vi ~/.docker/config.json
"""
{
    "proxies": {
        "default": {
            "httpProxy": "http://proxy.your.corp",
            "httpsProxy": "https://proxy.your.corp",
            "noProxy": "localhost,127.0.0.1,*.your.corp"
        }
    }
}
"""
$ service docker restart 

```

## git 

```python 
$ vi ~/.gitconfig
"""
[http]
      proxy = http://168.219.61.252:8080
      sslVerify = false

[https]
	proxy = http://168.219.61.252:8080
	sslVerify = false
"""


```

## 3. wget 

```
#~/.wgetrc  or /etc/wgetrc
use_proxy=yes
http_proxy=168.219.61.252:8080
https_proxy=168.219.61.252:8080

$ wget ... -e use_proxy=yes -e http_proxy=127.0.0.1:8080 ...
```



## 9. 확인 
```
set | grep -i proxy
```

---

## etc. Cert Installation

```
$ sudo mkdir /usr/share/ca-certificates/samsung
$ sudo cp samsung.crt /usr/share/ca-certificates/samsung/
$ sudo cp samsung.crt /etc/ssl/certs/
$ sudo dpkg-reconfigure ca-certificates
$ sudo update-ca-certificates
```
