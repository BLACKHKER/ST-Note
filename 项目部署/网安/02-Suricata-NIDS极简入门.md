### Suricata-NIDS极简入门



#### 一、安装Suricata

本文档默认你已经在CentOS 7.9上安装并配置好Wazuh的基础上进行。

##### 1.安装`epel-release`

```shell
yum install epel-release yum-plugin-copr
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936490.png" alt="image-20230308200047435" style="zoom:67%;" />

###### 中途会叫用户选择是否安装，输入y回车就行

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936051.png" alt="image-20230308200254319" style="zoom:67%;" />

###### 出现以下结果表明安装成功

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936264.png" alt="image-20230308200350637" style="zoom:67%;" />



##### 2.安装suricata

```shell
yum copr enable @oisf/suricata-6.0
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936021.png" alt="image-20230308200423579" style="zoom:67%;" />

###### 输入y继续安装，完成

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936288.png" alt="image-20230308200524833" style="zoom:67%;" />

###### 执行指令进行安装

```shell
yum install -y suricata
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936348.png" alt="image-20230308201147090" style="zoom:67%;" />

###### 完成安装

![image-20230308201204235](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936904.png)







### 二、使用Suricata功能

##### 1.修改Suricata配置文件（请先备份）

```shell
vi /etc/suricata/suricata.yaml
```

###### 确认18行是否包括你目前所在网段

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936409.png" alt="image-20230308203802836" style="zoom:67%;" />

###### 修改24行，将EXTERNAL_NET: "!$HOME_NET" 改为 EXTERNAL_NET: "any"

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936135.png" alt="image-20230308201528171" style="zoom:67%;" />

###### 修改68行，将 数字8修改为 8000 或其他较大的数字，减少stat.log文件大小

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936830.png" alt="image-20230308201609504" style="zoom:67%;" />

###### 修改1919行：将default-rule-path: /var/lib/suricata/rules 为 default-rule-path: /etc/suricata/rules

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936230.png" alt="image-20230308201728517" style="zoom:67%;" />



##### 2、定义预警类别和严重程度

进入目录  /etc/suricata 中并编辑 classification.config 文件，在末尾添加以下内容：

```config
config classification: web-status-error, Web服务器状态异常, 5
config classification: web-scan-attack, Web页面扫描攻击, 4
config classification: web-sql-injection, SQL注入攻击, 3
config classification: web-sql-injection, 连续SQL注入攻击, 1
config classification: web-xss-attack, XSS跨站攻击, 3
config classification: web-ssrf-attack, SSRF请求伪造, 2
config classification: web-shell-attack, 站点木马植入, 1
config classification: web-file-upload, 文件上传异常, 2
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936359.png" alt="image-20230308201929671" style="zoom: 67%;" />



##### 3、编写预警规则

进入目录  /etc/suricata/rules/ 中并添加文件名：suricata.rules 的新文件，编写以下规则：

```rules
alert http any any <> any 8080 (msg:"Web服务器404异常"; http.stat_code; content:"404"; classtype: web-status-error; sid: 561001; rev: 1;)

alert http any any <> any 8080 (msg:"频繁404状态码，疑似扫描"; http.stat_code; content:"404"; threshold: type both, track by_src, count 5, seconds 20; classtype: web-scan-attack; sid: 561002; rev: 1;)

alert http any any -> any 8080 (msg:"单次SQL注入攻击"; http.uri; pcre: "/union|select|from|updatexml|extract|database\(|version\(|information_schema|columns|--\s+|--\++|%20and%20|\s+or/i"; classtype: web-sql-injection; sid: 561101; rev: 1;)
```

![image-20230308202033329](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936705.png)



##### 4、测试预警是否生效

###### 进入/etc/suricata/目录

```shell
cd /etc/suricata/
```

###### 执行行一下指令启动suricata进行测试

```shell
suricata -c suricata.yaml -i ens33
```

###### 没有报错并出现以下内容表明配置成功

![image-20230308202255330](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936453.png)

###### 此时在新终端中监控预警文件，并进行攻击操作：

```shell
tail -f /var/log/suricata/fast.log
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936177.png" alt="image-20230308203957003" style="zoom:67%;" />

访问不存在的页面，触发404错误：http://192.168.145.130:8080/index.jspx

![image-20230308203847198](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936336.png)

连续触发404错误：

![image-20230320192449378](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936948.png)

SQL注入攻击：http://192.168.73.129:8080/index.jsp?id=-1 union select 1,2,3

![image-20230308204058423](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936963.png)







### 三、编辑以下更多规则进行测试

##### 编辑文件

```shell
vi /etc/suricata/rules/suricata.rules
```



##### 添加以下规则

```rules
# 木马上传或植入
alert http any any -> any 8080 (msg:"疑似上传PHP或JSP木马"; http.method; content:"POST"; http.content_type; content: "multipart/form-data"; http.request_body; content: "Content-Disposition"; http.request_body; pcre: "/eval|assert|system|exec|$_POST|$_GET|getInstance|getRuntime|ClassLoader/i"; classtype: web-file-upload; sid:561601; rev: 1;)

# XSS攻击
alert http any any -> any 8080 (msg:"疑似XSS攻击"; http.uri; pcre:"/<script>|javascript|alert|=http:|onload=|onclick=/i"; classtype: web-xss-attack; sid:561201; rev: 1;)

# SSRF攻击
alert http any any -> any 8080 (msg:"疑似SSRF攻击"; http.uri; content:"=dict|3A|"; nocase; classtype: web-ssrf-attack; sid:561301; rev: 1;)
alert http any any -> any 8080 (msg:"疑似SSRF攻击"; http.uri; content:"=gopher|3A|"; nocase; classtype: web-ssrf-attack; sid:561302; rev: 1;)
```

![image-20230308213058024](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936308.png)

> 只要满足上述正则表达式规则和对应字段内容，则Suricat就会检测到该攻击行为，并不需要服务器端真实存在漏洞。







### 四、Wazuh整合Suricata

##### 编辑Wazuh的配置文件ossec.conf

```shell
vi /var/ossec/etc/ossec.conf
```



##### 在最后添加对suricata预警目录下的eve.json的支持，即可将Suricat的预警采集到Wazuh中

```xml
<localfile>
    <log_format>json</log_format>
    <location>/var/log/suricata/eve.json</location>
</localfile>
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936599.png" alt="image-20230308204505460" style="zoom:67%;" />



##### 重启Wazuh生效

```shell
systemctl restart wazuh-manager
```



##### 实时监听预警信息

```shell
cd /var/ossec/logs/alerts/
tail -f alerts.log
```

![image-20230308212952626](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936751.png)

![image-20230308205110523](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201936781.png)

```
** Alert 1678365376.78544: - ids,suricata,
2023 Mar 09 04:36:16 localhost->/var/log/suricata/eve.json
Rule: 86601 (level 3) -> 'Suricata: Alert - Web服务器404异常'
{"timestamp":"2023-03-09T04:36:15.161962-0800","flow_id":498919820466647,"in_iface":"ens33","event_type":"alert","src_ip":"192.168.73.129","src_port":8080,"dest_ip":"192.168.73.1","dest_port":51474,"proto":"TCP","tx_id":0,"alert":{"action":"allowed","gid":1,"signature_id":561001,"rev":1,"signature":"Web服务器404异常","category":"Web服务器状态异常","severity":5},"http":{"hostname":"192.168.73.129","http_port":8080,"url":"/abc.jsp","http_user_agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36","http_content_type":"text/html","http_method":"GET","protocol":"HTTP/1.1","status":404,"length":702},"files":[{"filename":"/abc.jsp","sid":[],"gaps":false,"state":"CLOSED","stored":false,"size":702,"tx_id":0}],"app_proto":"http","flow":{"pkts_toserver":4,"pkts_toclient":4,"bytes_toserver":707,"bytes_toclient":1117,"start":"2023-03-09T04:35:55.104919-0800"}}
timestamp: 2023-03-09T04:36:15.161962-0800
flow_id: 498919820466647.000000
in_iface: ens33
event_type: alert
src_ip: 192.168.73.129
src_port: 8080
dest_ip: 192.168.73.1
dest_port: 51474
proto: TCP
tx_id: 0
alert.action: allowed
alert.gid: 1
alert.signature_id: 561001
alert.rev: 1
alert.signature: Web服务器404异常
alert.category: Web服务器状态异常
alert.severity: 5
http.hostname: 192.168.73.129
http.http_port: 8080
http.url: /abc.jsp
http.http_user_agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36
http.http_content_type: text/html
http.http_method: GET
http.protocol: HTTP/1.1
http.status: 404
http.length: 702
files: [{
		"filename":	"/abc.jsp",
		"sid":	[],
		"gaps":	false,
		"state":	"CLOSED",
		"stored":	false,
		"size":	702,
		"tx_id":	0
	}]
app_proto: http
flow.pkts_toserver: 4
flow.pkts_toclient: 4
flow.bytes_toserver: 707
flow.bytes_toclient: 1117
flow.start: 2023-03-09T04:35:55.104919-0800
```



```json
{
    "timestamp":"2023-03-09T04:36:15.161962-0800",
    "flow_id":498919820466647,
    "in_iface":"ens33",
    "event_type":"alert",
    "src_ip":"192.168.73.129",
    "src_port":8080,
    "dest_ip":"192.168.73.1",
    "dest_port":51474,
    "proto":"TCP",
    "tx_id":0,
    "alert":{
        "action":"allowed",
        "gid":1,
        "signature_id":561001,
        "rev":1,
        "signature":"Web服务器404异常",
        "category":"Web服务器状态异常",
        "severity":5
    },
    "http":{
        "hostname":"192.168.73.129",
        "http_port":8080,
        "url":"/abc.jsp",
        "http_user_agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36",
        "http_content_type":"text/html",
        "http_method":"GET",
        "protocol":"HTTP/1.1",
        "status":404,
        "length":702
    },
    "files":[{
        "filename":"/abc.jsp",
        "sid":[],
        "gaps":false,
        "state":"CLOSED",
        "stored":false,
        "size":702,
        "tx_id":0
    }],
    "app_proto":"http",
    "flow":{
        "pkts_toserver":4,
        "pkts_toclient":4,
        "bytes_toserver":707,
        "bytes_toclient":1117,
        "start":"2023-03-09T04:35:55.104919-0800"
    }
}
```

