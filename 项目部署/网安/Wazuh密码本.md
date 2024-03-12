## Wazuh密码本

### 密码

```shell
# Admin user for the web user interface and Wazuh indexer. Use this user to log in to Wazuh dashboard
  indexer_username: 'admin'
  indexer_password: 'y3nzNFiReNWpuLwv+v3YK0I8ByVduV7c'

# Wazuh dashboard user for establishing the connection with Wazuh indexer
  indexer_username: 'kibanaserver'
  indexer_password: 'Q55RuMeO7O*j4.Cwd0bWp9EC62awWUjG'

# Regular Dashboard user, only has read permissions to all indices and all permissions on the .kibana index
  indexer_username: 'kibanaro'
  indexer_password: 'XHcvcPk*oqd?6zhCHRL*oecvA2vB3DB+'

# Filebeat user for CRUD operations on Wazuh indices
  indexer_username: 'logstash'
  indexer_password: '8CI04b1b+4AvZdSkncqi7nMa+XOTBZcZ'

# User with READ access to all indices
  indexer_username: 'readall'
  indexer_password: '*?LD5N1Ro?T.mM3R10EMOz1E6*6EgZA*'

# User with permissions to perform snapshot and restore operations
  indexer_username: 'snapshotrestore'
  indexer_password: 'SQ0z6k7XWH?djPXp6?1ZNMrAA?6DvncH'

# Password for wazuh API user
  api_username: 'wazuh'
  api_password: '29+VblWchhraSbCIv7*ZJqSZBZiiU+J5'

# Password for wazuh-wui API user
  api_username: 'wazuh-wui'
  api_password: '4MS?+GbLm66CEX5qtQxy83a4ycNNPvYb'
```







### 找回密码

```shell
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```

![image-20230324104052442](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303241103299.png)

###### ※需要先切换到wazuh-install-files.tar包存在的路径，否则提示：无法 open: 没有那个文件或目录

![image-20230324103439724](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303241103369.png)

###### 先查询文件在哪个目录，并切换到该目录：

```shell
find / -name wazuh-install-files.tar
cd ......
```

![image-20230324103848283](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303241103665.png)







### 调用API

##### 获取Token(JWT)

```shell
curl -u <USER>:<PASSWORD> -k -X GET "https://<HOST_IP>:55000/security/user/authenticate"
```

###### 实例：	

```shell
curl -u wazuh:29+VblWchhraSbCIv7*ZJqSZBZiiU+J5 -k -X GET "https://192.168.145.130:55000/security/user/authenticate"

curl -u wazuh-wui:4MS?+GbLm66CEX5qtQxy83a4ycNNPvYb -k -X GET "https://192.168.145.130:55000/security/user/authenticate"
```

![image-20230324104356367](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303241103681.png)



##### 携带Token使用以下格式调用任何API

```shell
curl -k -X <METHOD> "https://<HOST_IP>:55000/<ENDPOINT>" -H "Authorization: Bearer <YOUR_JWT_TOKEN>"
```

###### 实例：调用manager的状态API：

```shell
curl -k -X GET "https://192.168.145.130:55000/manager/status" -H "Authorization: Bearer eyJhbGciOiJFUzUxMiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ3YXp1aCIsImF1ZCI6IldhenVoIEFQSSBSRVNUIiwibmJmIjoxNjc5NTgzNDkwLCJleHAiOjE2Nzk1ODQzOTAsInN1YiI6IndhenVoIiwicnVuX2FzIjpmYWxzZSwicmJhY19yb2xlcyI6WzFdLCJyYmFjX21vZGUiOiJ3aGl0ZSJ9.AIV1fNZ4nllOV56YBNp8wh1li0r0w1xDG3AHc1iNGfJjlpvDCQP4IPS7Y132MI05Of6rGpCU9gGV2SVqBNI48zaOATfFMdKb-1UvU1EVLjNpz-3fdJQfZiwNzb-WSeaawD7zovOmsCMqXm0sPfVBTYrivz_BCH_21fBs0ndXCHyIRiRk"
```

