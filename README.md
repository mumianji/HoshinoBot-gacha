# HoshinoBot-gacha
是Ice-Cirno/[HoshinoBot](https://github.com/Ice-Cirno/HoshinoBot)中抽卡部分的功能需要的配置文件中的一部分。

## 使用

各取所需即可。

### v1

v1版本相关文件：priconne.py

### v2

v2版本相关文件：_pcr_data.py

# 抄了一份部署教程：

## How to install HoshinoBot：

system>=CentOS 7.6

### python install

```bash
yum -y update&&yum -y groupinstall "Development tools"&&yum -y install wget zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc* libffi-devel make git java vim screen&&wget https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tgz&&tar -zxvf Python-3.8.5.tgz&&cd Python-3.8.5&&./configure&&make&&make install&&pip3 install --upgrade pip&&cd
```

### CQHTTPMirai install

```bash
mkdir mirai&&cd mirai&&wget https://github.com/yyuueexxiinngg/cqhttp-mirai/releases/download/0.2.1/cqhttp-mirai-0.2.1-embedded-all.jar&&java -jar cqhttp-mirai-0.2.1-embedded-all.jar
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
java -jar cqhttp-mirai-0.2.1-embedded-all.jar

#Then,use `Ctrl+a,d` to keep this process
```

## HoshinoBot install 
```bash
cd&&git clone https://github.com/Ice-Cirno/HoshinoBot.git
cd HoshinoBot&&cp -r hoshino/config_example /hoshino/config
pip3 install -r requirements.txt

#custom your bot setting
vim hoshino/config/__bot__.py

#install other pack（Optional，run faster）
pip3 install msgpack ujson python-Levenshtein

screen -S Hoshino
python3 run.py

#Then,use `Ctrl+a,d` to keep this process
```

## yobot install

### I suggest you use the normal method to install

```bash
cd ~&&git clone https://github.com/pcrbot/yobot.git
pip3 install -r yobot/scr/client/requirements.txt
screen -S yobot
python3 yobot/scr/client/main.py
sh yobot/scr/client/yobotg.sh

#Then,use `Ctrl+a,d` to keep this process
```

Then, you need to modify the configuration so that the yobot is connected

```bash
vim mirai/plugins/setting.yml
```

You need to cancel the comment from line 21 to line 27 and reboot mirai

### You can also install yobot in the form of plugins

```bash
cd ~/HoshinoBot/hoshino/modules&&mkdir yobot&&cd yobot
git init&&git submodule add https://github.com/pcrbot/yobot.git
pip3 install -r scr/client/requirements.txt

vim ~HoshinoBot/hoshino/config/__bot__.py
#add `yobot` to the MODULE_ON and reboot HoshinoBot

#shut down your HoshinoBot
vim ~HoshinoBot/hoshino/modules/yobot/yobot/scr/client/yobot_data/yobot_config.json
#you need to change '9222' in 'public_address' to '8080' and reboot Hoshinobot
```

Finish.
