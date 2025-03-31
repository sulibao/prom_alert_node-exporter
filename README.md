# prom_alert_node-exporter

以下各文件用于通过docker-compose进行prometheus(email)+alertmanager+node-exporter的快速部署

用法如下：

```
docker-compose <-f docker-compose.yml> up -d
```

## docker-compose.yml文件

定义了部署所需要的镜像和配置文件参数

## alertmanager.yml文件

定义了告警邮件配置参数

```
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



## rules.yml

定义了告警规则配置

## blackbox.yml

定义了黑盒配置文件参数

## prometheus.yml

定义了prometheus-job和告警文件等配置

## 访问方式

```
prometheus：http://IP:3000

grafana：http://IP:9090

alertmanager：http://IP:9093
```

