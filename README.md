# springboot nginx cluster


# 目标:

``` python
  8081&8082 均衡 8083备份(在8081&8082都down机时执行)

  server 127.0.0.1:8081 weight=4 max_fails=2 fail_timeout=30s;
  server 127.0.0.1:8082 weight=4 max_fails=2 fail_timeout=30s;
  server 127.0.0.1:8083 backup;
```

## 配置源码见:  

``` python
  ./haproxy-loadbance.zip
  ./nginx-loadbance.zip
```
  
  
## ha&ng结果比对:


### backup

- **haproxy**
<image src="src/main/resources/ha-pics/backup.jpeg"></image>
- **nginx**
<image src="src/main/resources/ng-pics/backup.jpeg"></image>


### config

- **haproxy**
<image src="src/main/resources/ha-pics/config.jpeg"></image>
- **nginx**
<image src="src/main/resources/ng-pics/config.jpeg"></image>


### roundrobin

- **haproxy**

<image src="src/main/resources/ha-pics/roundrobin.png"></image>

- **nginx**

<image src="src/main/resources/ng-pics/roundrobin.png"></image>

### test

- **happroxy**

<image src="src/main/resources/ha-pics/test.jpeg"></image>
- **nginx**

<image src="src/main/resources/ng-pics/test.png"></image>

