> [!NOTE]
> 文章来源：[拾光](https://blog.mado.us.kg/)

### 1. 创建 Telegram Bot 并获取 Token
首先，需要在 Telegram 上创建一个 Bot 并获取其 Token。你可以通过以下步骤创建一个 Bot：

打开 Telegram，搜索 `@Botfather` 并开始对话。

发送 `/start` 开始。

发送 `/newbot` 创建一个新 Bot。

按照提示给你的 Bot 取一个名字和用户名。

创建完成后，你会收到一个 Token，用于通过 Telegram API 发送消息。

token样式类似`123455:jklsdfjlksdjklfjlka`

### 2. 获取你的 Chat ID
你需要获取你的 Telegram Chat ID，用于将消息发送到特定的聊天窗口。可以通过以下步骤获取：

在 Telegram 中搜索并开始与 [@userinfobot](https://t.me/userinfobot) [(https://t.me/userinfobot)](https://t.me/userinfobot)对话。

发送 `/start`。

你会收到一条包含你 Chat ID 的消息。

### 3.脚本修改
需要自己修改里面的参数

命令行使用以下命令,domains文件夹下执行(其他目录也行，自己改下参数路径）
#### 步骤一：使用 cat 命令创建脚本文件
```
# 使用 cat 命令创建脚本文件
cat << 'EOF' > Serv00-Renew.sh
#!/bin/bash

download_python_file() {
    local url="$1"
    local filename="$2"
    if command -v curl &> /dev/null; then
        curl -L "$url" -o "$filename"
    elif command -v wget &> /dev/null; then
        wget -O "$filename" "$url"
    else
        echo "错误：未找到 curl 或 wget。请安装其中之一以继续。"
        exit 1
    fi
    
    if [ $? -eq 0 ]; then
        echo "成功下载 $filename"
    else
        echo "下载 $filename 失败"
        exit 1
    fi
}

install_required_modules() {
    local filename="$1"
    echo "正在分析 $filename 所需的模块..."
    
    modules=$(grep -E "^import |^from " "$filename" | sed -E 's/^import //; s/^from ([^ ]+).*/\1/' | sort -u)
    
    for module in $modules; do
        if ! python3 -c "import $module" 2>/dev/null; then
            echo "正在安装模块: $module"
            pip3 install "$module"
        fi
    done
}

# 设置环境变量
export HOSTNAME="你的name.serv00.net"
export USERNAME="你的name"
export URL="http://你的name.serv00.net" #前提是你没有删除自己的默认网站，删除了就用自己搭建应用的网址
export SSH_PASSWORD="密码"
export BOT_TOKEN="2342342342342:dsfsddfsdfsfdfsfsdfsd" #上面获取的
export CHAT_ID="234234234"  #上面获取的

download_python_file "https://raw.githubusercontent.com/elderSword/Serv00_auto_script/master/Auto_connect_SSH-TG.py" "Auto_connect_SSH-TG.py"

install_required_modules "Auto_connect_SSH-TG.py"

pip uninstall --user telegram
pip install --user python-telegram-bot


python3 ~/domains/Auto_connect_SSH-TG.py
EOF
```
**Auto_connect_SSH-TG.py 必须使用我修改的路径下载，原来的脚本ssh有问题**
#### 步骤二：添加可执行权限
```
chmod +x Serv00-Renew.sh
```
#### 步骤三：执行脚本
```
./Serv00-Renew.sh
```

![349980923-249c4b00-5467-42a3-9c5d-737452a12b5d](https://github.com/user-attachments/assets/66e7dbfb-ae80-43d5-aa4a-7cb7204c55bb)
如果是上图，最好先看看URL参数是否合适
正常是下图
![2](https://github.com/user-attachments/assets/cc69961f-c9b2-494f-8cd3-8ff9999f4e33)

### 4.添加corn job
这个间隔自己控制，我设置的是1小时检测一次
<img width="1116" alt="3" src="https://github.com/user-attachments/assets/516179c1-00e1-4b0c-b817-809245edb18d">

选`Hourly`
command： 
```
sh ~/domains/Serv00-Renew.sh
```