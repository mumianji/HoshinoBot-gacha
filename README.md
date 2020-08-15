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

system >= CentOS 7.6

### 安装 python3.8

```bash
yum -y update&&yum -y groupinstall "Development tools"&&yum -y install wget zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc* libffi-devel make git java vim screen&&wget https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tgz&&tar -zxvf Python-3.8.5.tgz&&cd Python-3.8.5&&./configure&&make&&make install&&pip3 install --upgrade pip&&cd
```

### 安装 CQHTTPMirai

```bash
mkdir mirai&&cd mirai&&wget https://github.com/yyuueexxiinngg/cqhttp-mirai/releases/download/0.2.1/cqhttp-mirai-0.2.1-embedded-all.jar&&java -jar cqhttp-mirai-0.2.1-embedded-all.jar
#使用 Ctrl+C 关闭这个进程

vim plugins/setting.yml
```

### CQHTTPMirai 的配置文件示例

```yml
debug: false
'你用来做bot的QQ账号':
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

#然后，使用 Ctrl+a,d 挂起这个窗口
```

## 安装 HoshinoBot

```bash
cd&&git clone https://github.com/Ice-Cirno/HoshinoBot.git
cd HoshinoBot&&cp -r hoshino/config_example /hoshino/config
pip3 install -r requirements.txt

#自定义你的 bot 设置
vim hoshino/config/__bot__.py

#安装其他非必须依赖（可选，使 bot 运行更丝滑）
pip3 install msgpack ujson python-Levenshtein

screen -S Hoshino
python3 run.py

#然后，使用 Ctrl+a,d 挂起这个窗口
```

## 安装 yobot

### 使用 Python 运行 yobot 源码 (推荐)

```bash
cd ~&&git clone https://github.com/pcrbot/yobot.git&&pip3 install -r yobot/scr/client/requirements.txt
screen -S yobot
python3 yobot/scr/client/main.py
sh yobot/scr/client/yobotg.sh

#然后，使用 Ctrl+a,d 挂起这个窗口
```

然后，更改 CQHTTPMirai 的配置文件使得 yobot 能被 mirai 连接

```bash
vim mirai/plugins/setting.yml
```

取消掉第 22 行到第 28 行的注释

### 作为 Hoshino 的插件运行 (可选)

```bash
cd ~/HoshinoBot/hoshino/modules&&mkdir yobot&&cd yobot
git init&&git submodule add https://github.com/pcrbot/yobot.git
pip3 install -r scr/client/requirements.txt

vim ~HoshinoBot/hoshino/config/__bot__.py
#在 MODULES_ON 里添加 'yobot'

#关掉Hoshino，然后
vim ~HoshinoBot/hoshino/modules/yobot/yobot/scr/client/yobot_data/yobot_config.json
#修改 'public_address' 中的端口，9222 修改为 8080
```

## 安装以 Hoshino 为框架的其他功能

```bash
cd ~/HoshinoBot/hoshino/modules&&mkdir custom&&cd custom&&git init&&git clone https://github.com/Lancercmd/Landsol-Distrust.git&&git clone https://github.com/Lancercmd/Reloader.git

vim ~HoshinoBot/hoshino/config/__bot__.py
#在 MODULES_ON 里添加 'custom'
```

## 安装 CQ-picsearcher-robot

### 安装 nodejs

```bash
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
yum install nodejs -y
```

### 修改 CQHTTPMirai 的配置文件使得 Mirai 能连接上 CQ-picsearcher-robot

```bash
vim mirai/plugins/setting.yml
```

第三十行 enable 修改为 true ，并重启 mirai 

### 安装 CQ-picsearcher-robot

```bash
https://github.com/Tsuk1ko/cq-picsearcher-bot.git&&cd cq-picsearcher-bot&&npm install -g yarn&&npm install -g pm2&&yarn install

#自定义 bot 配置
cp config.default.json config.json&&vim config.json
#必要的修改：
#第 15 行 admin 字段中的 -1 修改为你自己的QQ号(作为主人)

#启动
yarn start

#bot会在20秒内通知你 已上线 
```

Finish.
