> [!NOTE]
> 文章来源：[北京大学](https://its.pku.edu.cn/faq_fail2ban.jsp)
       
对于校园网中近期发现的针对Linux系统的ssh暴力破解行为，可以通过安装fail2ban加强防护。 fail2ban是一款入侵防御软件，能够运行在大多数Linux服务器上，保护计算机服务器免受暴力破解的攻击。fail2ban启动后会通过检测系统行为日志识别暴力破解行为，对于在短时间内多次未能通过身份验证的请求，fail2ban会自动调用系统自带的防火墙或包管理框架（如iptables或tcp wrapper等）进行封禁。

在安装fail2ban之前，建议将ssh服务配置为[**通过密钥登录并禁止密码登录**](https://www.xiapilu.com/web/web-tutorial/ssh-login-key.html#:~:text=1%E3%80%81%E7%99%BB%E5%BD%95VPS%E4%B8%BB%E6%9C%BA%E7%94%9F)。这样既可以增强安全性，也可以避免fail2ban启动后因忘记密码或输错密码导致正常登录被封禁。
## 一、fail2ban 的安装及部署方法

步骤1. 更新软件源

```
sudo apt-get update
```

步骤2. 安装fail2ban

```
sudo apt-get install -y fail2ban
```

步骤3. 启动fail2ban服务并设置开机自启

```
sudo systemctl start fail2ban

sudo systemctl enable fail2ban
```

步骤4. 配置 fail2ban jail 规则

用任意文本编辑器打开 `/etc/fail2ban/jail.local` 用以下内容替换原有配置：

`Gmeek-html<img src="https://its.pku.edu.cn/img/faq_fail2ban-1.png">`

**注: 如认为60秒内失败2次过于严格，可根据使用习惯将maxretry设置为稍大一点的数值，越小安全性越高**

步骤5. 保存并关闭该文件。

使用以下命令重新启动fail2ban

```
sudo systemctl restart fail2ban
```

## 二、fail2ban的测试及关闭服务方法

查看当前封禁IP：

```
sudo fail2ban-client status sshd
```

解禁某一IP:

```
sudo fail2ban-client set sshd unbanip IP_ADDRESS
```

停止fail2ban服务：

```
sudo systemctl stop fail2ban
```

关闭fail2ban服务：

```
sudo systemctl disable fail2ban
```

## 三、更多相关知识请参考

仓库地址：[https://github.com/fail2ban/fail2ban](https://github.com/fail2ban/fail2ban)

项目主页：[https://www.fail2ban.org/wiki/index.php/Main_Page](https://www.fail2ban.org/wiki/index.php/Main_Page)

AWS博客介绍：[https://aws.amazon.com/cn/blogs/china/open-source-tool-to-protect-ec2-instances-fail2ban](https://aws.amazon.com/cn/blogs/china/open-source-tool-to-protect-ec2-instances-fail2ban)
