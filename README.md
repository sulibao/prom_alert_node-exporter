# prom_alert_node-exporter

The following files are used for the rapid deployment of prometheus(email)+alertmanager+node-exporter through docker-compose. Please modify the information about mount data directory and access port.

Use it as follows：

```sh
docker-compose <-f docker-compose.yml> up -d
```

## 1.docker-compose.yml

Defines the image and configuration file parameters required for deployment

## 2.alertmanager.yml

Alert mail configuration parameters are defined

```yaml
global:
  resolve_timeout: 5m
  smtp_smarthost: 'smtp.qq.com:465'   #Mail server address, need to connect to the port
  smtp_from: 'xxx'                #Email address
  smtp_auth_username: 'xxx'       #Email authentication user address, usually the same as smtp_from
  smtp_auth_password: 'xxx'       #邮Email authorization code
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
  - to: 'xxx'               #Alert receiving email address
```



## 3.rules.yml

An alarm rule configuration is defined

## 4.blackbox.yml

The black-box profile parameters are defined

## 5.prometheus.yml

Configurations such as prometheus-job and alarm files are defined

## 6.Address of access

```sh
prometheus：http://IP:3000

grafana：http://IP:9090

alertmanager：http://IP:9093
```

## 7.The json for the simple grafana panel is as follows

```sh
#Just import the json file from the grafana page

disk.json：Server disk usage is shown

node-exporter-grafana.json：Server disk, io, cpu usage is displayed
```

## 8.Involved image package (X86 version, Baidu Net Disk)

```sh
docker load -i prom_alert_exporter_images.tgz
```

Links: https://pan.baidu.com/s/1xJI3sY5gvx27CWNmFno6Xw?pwd=dqq6 

Extraction code: dqq6


