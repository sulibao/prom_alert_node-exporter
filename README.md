# prom_alert_node-exporter

The following files are used for the rapid deployment of prometheus(email)+alertmanager+node-exporter through docker-compose. Please modify the information about mount data directory and access port.

Use it as follows：

```sh
docker-compose <-f docker-compose.yml> up -d
```

## 1.docker-compose.yml

Defines the image and configuration file parameters required for deployment,If you need to modify the image and port, please edit this file and modify it yourself.

## 2.alertmanager.yml

Alert mail configuration parameters are defined

```yaml
global:
  resolve_timeout: 5m
  smtp_smarthost: 'smtp.qq.com:465'   #Mail server address, need to connect to the port
  smtp_from: 'xxx'                #Email address
  smtp_auth_username: 'xxx'       #Email authentication user address, usually the same as smtp_from
  smtp_auth_password: 'xxx'       #Email authorization code
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

This is where you define the alert rules you need.

## 4.blackbox.yml

The black-box profile parameters are defined

## 5.prometheus.yml

This is where monitoring, alerting, and other tasks are configured.

## 6.Address of access

```sh
prometheus：http://IP:3000

grafana：http://IP:9090

alertmanager：http://IP:9093
```

## 7.Data source and data panel initialization configuration

```yaml
#The data sources are configured in the config folder。
(1)datasources.yaml
apiVersion: 1
deleteDatasources:
  - name: Prometheus
    orgId: 1
datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    orgId: 1
    uid: prometheus
    url: http://192.168.2.193:9090   #The address here is the address of your prometheus service。
    isDefault: true
(2)default-provider.yaml
apiVersion: 1
providers:
- name: 'default-provider'
  orgId: 1
  folder: dashboards
  folderUid: ''
  type: file
  disableDeletion: false
  editable: true
  updateIntervalSeconds: 10
  options:
    path: /etc/grafana/dashboards     
    #Here you specify the path from the container to read the dashboards file, which you can find in the grafana mount in the docker-compose.yaml file
    foldersFromFilesStructure: true
#The dashboards file config the two initial node monitor panels
disk.json：Server disk usage is shown
node-exporter-grafana.json：Server disk, io, cpu usage is displayed
```
