# prom_alert_node-exporter

以下各文件用于通过docker-compose进行prometheus(email)+alertmanager+node-exporter的快速部署，涉及挂载数据目录和访问端口等信息请自行修改。

用法如下：

```sh
docker-compose <-f docker-compose.yml> up -d
```

## 1.docker-compose.yml文件

定义了部署所需要的镜像和配置文件参数

## 2.alertmanager.yml文件

定义了告警邮件配置参数

```yaml
global:
  resolve_timeout: 5m
  smtp_smarthost: 'smtp.qq.com:465'   #邮件服务器地址
  smtp_from: 'xxx'                #邮件发送地址
  smtp_auth_username: 'xxx'       #邮箱认证用户地址，一般和smtp_from一致
  smtp_auth_password: 'xxx'          #邮箱授权码
  smtp_require_tls: false
 
route:
  group_by: ['alertname']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 12h
  receiver: 'test-alertmanager'
 
receivers:
- name: 'test-alertmanager'
  email_configs:
  - to: 'xxx'               #告警接收邮箱地址
```



## 3.rules.yml

定义了告警规则配置

## 4.blackbox.yml

定义了黑盒配置文件参数

## 5.prometheus.yml

定义了prometheus-job和告警文件等配置

## 6.访问方式

```sh
prometheus：http://IP:3000

grafana：http://IP:9090

alertmanager：http://IP:9093
```

## 7.涉及简单grafana面板json如下

```sh
#在grafana页面import json文件即可

disk.json：服务器磁盘使用展示

node-exporter-grafana.json：服务器磁盘、io、cpu等使用展示
```

## 8.涉及镜像包(X86版本，Baidu Net Disk)

```sh
docker load -i prom_alert_exporter_images.tgz
```

链接: https://pan.baidu.com/s/1xJI3sY5gvx27CWNmFno6Xw?pwd=dqq6 

提取码: dqq6