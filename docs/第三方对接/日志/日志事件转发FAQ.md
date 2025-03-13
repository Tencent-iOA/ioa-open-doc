### 1、如何配置 syslog 转发服务器接收日志

1. 在文件 `/etc/rsyslog.conf` 中开启 UDP 接受

```
# Provides UDP syslog reception
$ModLoad imudp
$UDPServerRun 514
```

2. 在文件 `/etc/sysconfig/rsyslog` 中加上允许接受外来日志

```
SYSLOGD_OPTIONS="-r -c 2"
```

3. 重启syslog服务

```bash
systemctl restart rsyslog

# check status
systemctl status rsyslog
lsof -i :514
```

### 2、如何配置 http 转发服务器接收日志

1. 在服务器上搭建python3环境

2. 安装Flask插件

3. 运行如下python脚本：

```python
from flask import Flask
from flask import request
import logging
import json
app = Flask(__name__)
logging.basicConfig(filename='header_trace.log', level=logging.DEBUG)


@app.route('/', methods=['GET', 'POST'])
def hello_world():
    # header_str = request.headers.__repr__()
    # logging.info(f"headers ---> {header_str}")
    request_data = request.get_json()
    logging.info(f"msg revieve: {request_data}")
    return "ok"


if __name__ == '__main__':
    app.run(port=8081, host='0.0.0.0', debug=True)
```

### 3、如何配置 nsq 转发服务器接收日志

使用docker搭建nsq，参照：https://nsq.io/deployment/docker.html

搭建完成后使用如下方式验证：

1. 发送日志及创建topic：curl -d 'hello world ' 'http://127.0.0.1:4151/pub?topic=test'

2. 查看对应的topic：curl 'http://127.0.0.1:4161/topics'

3. 在浏览器打开 http://127.0.0.1:4171/ 来访问 NSQ 的管理后台，查看统计数据。

4. 使用如下脚本消费nsq消息来查看收到的具体内容，允许脚本后在同目录下生成一个nsq_trace.log记录nsq接收到的信息：

```python
import nsq

import logging l

ogging.basicConfig(filename='nsq_trace.log', level=logging.DEBUG)

def handler(message):

    print(message)

    print(message.body)

    logging.info(f"msg revieve: {message}:{message.body}")

    return True

r = nsq.Reader(message_handler=handler,nsqd_tcp_addresses=['9.135.97.192:4150'],topic='test',channel='asdfxx', lookupd_poll_interval=15)

nsq.run()
```

### 4、没有收到日志推送常见问题与排查路径

1. 是否有日志产生：是否有对触发对应日志的操作发生，可以同时查看控制台是否有对应日志

2. 服务端查看接收情况：在对应的消息队列或文件种查看，http的日志在脚本同路径下的 header_trace.log 中查看；syslog 的日志在 /var/log/messages 中查看

3. 接收服务器是否配置错误：例如 syslog 中 `/etc/rsyslog.conf` 配置错误，kafka 中 topic 是否创建或者允许自动创建等。可以使用本文上面的示例配置进行测试

4. 接收服务器网络配置是否放通：
    - 使用netstat -anp查看对应的监控端口是否运行中
    - 使用service iptables status 查看防火墙是否关闭
    - 查看防火墙策略是否屏蔽了对应的端口
    - 查看监控端口的协议是否为tcp，如果不是则创建服务时在参数中增加–net=host即可

5. 转发策略是否包含对应日志，可以查看 “日志事件转发” 文中的 “转发策略与命令字对应表”

6. 日志转发服务异常：可以分别在转发服务器与接收服务器端抓包查看是否有对应转发包，或者查看 event-deliver 服务日志是否有异常