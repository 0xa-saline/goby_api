# gobies 对应的api



### 0. 获取api信息

```
strings goby-cmd |grep ":8361/api/v1"
```

### 1. 开启api

```
./goby-cmd  -mode api -bind 0.0.0.0:8361
```

### 2. 开启扫描任务
```
curl 127.0.0.1:8361/api/v1/startScan -d '{"asset":{"ips":["10.10.10.0/24"], "ports":"", "vulnerability": {"type": "2"}}}'
```
返回

```
{"statusCode":200,"messages":"","data":{"taskId":"20200326164404"}}
```

### 3. 查询漏洞

```
curl 127.0.0.1:8361/api/v1/vulnerabilitySearch -d '{"type": "ip", "query": "taskid=20200326164404"}'
```
返回

```
{"statusCode":200,"messages":"","data":{"total":{"ips":0,"vulnerabilities":0},"lists":null}}
```

### 4. 其他调用


```
查看全部任务
Fetch tasks:  curl 127.0.0.1:8361/api/v1/tasks 

开启扫描
Start scan: curl 127.0.0.1:8361/api/v1/startScan -d '{"asset":{"ips":["10.10.10.0/24"], "ports":"1-1024"}}' 

增加poc扫描
curl 127.0.0.1:8361/api/v1/startScan -d '{"asset":{"ips":["10.10.10.0/24"], "ports":"", "vulnerability": {"type": "2"}}}'

获取IP信息
curl 127.0.0.1:8361/api/v1/getIPInfo -d '{"taskid": "taskiduuid", "ip": "10.10.10.22"}' 

资产搜索
curl 127.0.0.1:8361/api/v1/assetSearch -d '{"query":{{ queryencode $.Query }} }'

查看子类别
curl 127.0.0.1:8361/api/v1/getChildrenCategory -d '{"query":{{ queryencode $.Query }} }'

查看扫描进度
curl 127.0.0.1:8361/api/v1/getProgress -d '{"taskid":"taskiduuid"}' 

资产搜索
curl 127.0.0.1:8361/api/v1/assetSearch -d '{"query":"taskid=taskiduuid"}'

继续扫描
curl 127.0.0.1:8361/api/v1/resumeScan -d '{"taskid":"taskiduuid"}' 

停止扫描
curl 127.0.0.1:8361/api/v1/stopScan -d '{"taskid":"taskiduuid"}' 

获取类别
curl 127.0.0.1:8361/api/v1/getValueCategory -d '{"taskid":"20200326162304"}' 

获取资产详情
curl 127.0.0.1:8361/api/v1/assetDetail -d '{"type": 0, "query": "taskid=taskiduuid"}' 

获取poc信息
curl 127.0.0.1:8361/api/v1/getPocs -d '{"taskid": "taskiduuid"}' 

获取poc详情
curl 127.0.0.1:8361/api/v1/getPOCInfo -d '{"vulname": "{{ .Name }}"}'

漏洞搜索
curl 127.0.0.1:8361/api/v1/vulnerabilitySearch -d '{"type": "ip", "query": "taskid=taskiduuid"}' 

测试exp
curl 127.0.0.1:8361/api/v1/debugExp -d '{"hostinfo":"{{ .HostInfo }}", "vulfile":"{{ .FileName }}"}'
```

### 4. gobies相关
  
  a. 下载地址 https://gobies.org/#dl
  b. 更新说明 https://gobies.org/updates.html
