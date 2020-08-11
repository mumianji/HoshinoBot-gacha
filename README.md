# HoshinoBot-gacha
是Ice-Cirno/[HoshinoBot](https://github.com/Ice-Cirno/HoshinoBot)中抽卡部分的功能需要的配置文件中的一部分。

## 使用

### v1

默认分支是v1，若您的Hoshino是v1您可以直接替换相应文件。

### v2

若您的Hoshino是v2版本，您需要切换到v2分支替再替换相应文件。

抄了一份部署教程：

## How to install HoshinoBot：

system>=CentOS 7.6

### python install

```bash
yum -y update&&yum -y groupinstall "Development tools"&&yum -y install wget zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc* libffi-devel make git java vim screen&&wget https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tgz&&tar -zxvf Python-3.8.5.tgz&&cd Python-3.8.5&&./configure&&make&&make install&&pip3 install --upgrade pip&&cd
```

### miraiOK install

```bash
mkdir mirai&&cd mirai&&wget https://github.com/yyuueexxiinngg/cqhttp-mirai/releases/download/0.2.0/cqhttp-mirai-0.2.0-fix1-embedded-all.jar&&java -jar cqhttp-mirai-0.2.0-fix1-embedded-all.jar
#Then use `Ctrl+C` to exit this process
vim plugins/setting.yml
```

### config of CQHTTPMirai

```yml
debug: false
'your bot account':
  http:
    enable: false
    host: 0.0.0.0
    port: 5700
    accessToken: ""
    postUrl: ""
    postMessageFormat: string
    secret: ""
  ws_reverse:
    - enable: true
      postMessageFormat: string
      reverseHost: 127.0.0.1
      reversePort: 8080
      accessToken: ""
      reversePath: /ws
    #   reverseApiPath: /api
    #   reverseEventPath: /event
      useUniversal: true
      reconnectInterval: 3000
    # - enable: true
    #   postMessageFormat: string
    #   reverseHost: 127.0.0.1
    #   reversePort: 9222
    #   reversePath: /ws
    #   useUniversal: false
    #   reconnectInterval: 3000
  ws:
    enable: false
    postMessageFormat: string
    accessToken: ""
    wsHost: "0.0.0.0"
    wsPort: 6700

```

```bash
screen -S mirai
java -jar cqhttp-mirai-0.2.0-fix1-embedded-all.jar
```

## Estonteco install 
```bash
cd&&git clone https://github.com/Ice-Cirno/HoshinoBot.git
cd HoshinoBot&&cp -r hoshino/config_example/hoshino/config
pip3 install -r requirements.txt
screen -S Hoshino
python3 run.py
```

Finish.
