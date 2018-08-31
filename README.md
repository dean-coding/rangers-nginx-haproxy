# springboot nginx & haproxy 负载均衡比对


# 目标:

  8081&8082 均衡 8083备份(在8081&8082都down机时执行)

  server 127.0.0.1:8081 weight=4 max_fails=2 fail_timeout=30s;
  server 127.0.0.1:8082 weight=4 max_fails=2 fail_timeout=30s;
  server 127.0.0.1:8083 backup;

## 配置源码见:  

  ./haproxy-loadbance.zip
  ./nginx-loadbance.zip
  
## 结果比对:
  ./resource/ha-pis/**
  ./resource/ng-pis/**