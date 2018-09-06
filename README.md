# springboot nginx & haproxy 负载均衡比对

	一文一言: 骑自行车的再努力也追不上路虎,说明,平台很重要

# 简介:

 <image src="src/main/resources/ha-ng-compare.png" width="60%" height="600px"></image>
	
# 测试目标:

```source-python
  实现8081&8082 均衡 8083备份(在8081&8082都down机时执行)

  server 127.0.0.1:8081 weight=4 max_fails=2 fail_timeout=30s;
  server 127.0.0.1:8082 weight=4 max_fails=2 fail_timeout=30s;
  server 127.0.0.1:8083 backup;
```

## 环境:

haproxy官网: https://www.haproxy.org/

nginx官网: https://nginx.org/
  
1.安装: 选择对应os的版本离线安装,选择性配置环境变量
 ```python
  在线安装示例:
  > linux: # yum install haproxy
  > mac: # brew install haproxy
 ``` 
	  
2.版本:
最终目的,成功使用cli命令客户端
 ```python
root:haproxy mac$ haproxy -v
HA-Proxy version 1.8.7 2018/04/07
Copyright 2000-2018 Willy Tarreau <willy@haproxy.org>

root:haproxy mac$ nginx -V
nginx version: nginx/1.13.10
built by clang 9.0.0 (clang-900.0.39.2)
built with OpenSSL 1.0.2n  7 Dec 2017 (running with OpenSSL 1.0.2o  27 Mar 2018)
TLS SNI support enabled
configure arguments: --prefix=/usr/local/....
```
3.配置:(详细配置见源码文件)

4.手动方式启动:

	haproxy
	
<image src="src/main/resources/ha-pics/config.jpeg"></image>

 ```python
haproxy -f /usr/local/haproxy-loadbalance/ha01/haproxy.conf
如上述的配置:
stats-ui地址(stats uri & bind 配置): localhost:9099/haproxy-stats
输入用户名密码(stats auth配置):root/root
```

<image src="src/main/resources/ha-pics/haproxy-stats.png"></image>

	nginx
<image src="src/main/resources/ng-pics/config.jpeg"></image>
 ```python
nginx -c /usr/local/nginx-loadbalance/ng01/nginx.conf
```

## ha&ng结果比对:

### backup

	haproxy
	
<image src="src/main/resources/ha-pics/backup.jpeg" width="60%"  height="400px"></image>

	nginx
	
<image src="src/main/resources/ng-pics/backup.jpeg" width="60%" height="500px"></image>


### roundrobin

	haproxy

<image src="src/main/resources/ha-pics/roundrobin.png" height="400px"></image>
	
	nginx
	
<image src="src/main/resources/ng-pics/roundrobin.png" height="400px"></image>

### test

	happroxy

<image src="src/main/resources/ha-pics/test.jpeg" width="60%"></image>

	nginx

<image src="src/main/resources/ng-pics/test.png" width="60%"></image>

## 配置源码见:  

``` python
  ./haproxy-loadbance.zip
  ./nginx-loadbance.zip
```
