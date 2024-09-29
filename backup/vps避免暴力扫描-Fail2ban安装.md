vps避免暴力扫描-Fail2ban安装
----------------------------

# 一、fail2ban 的安装及部署方法

## 步骤1. 更新软件源

```
sudo apt-get update
```

## 步骤2. 安装fail2ban

```
sudo apt-get install -y fail2ban
```

## 步骤3. 启动fail2ban服务并设置开机自启

```
sudo systemctl start fail2ban

sudo systemctl enable fail2ban
```

## 步骤4. 配置 fail2ban jail 规则

用任意文本编辑器打开 `/etc/fail2ban/jail.local` 用以下内容替换原有配置：

**注: 如认为60秒内失败2次过于严格，可根据使用习惯将maxretry设置为稍大一点的数值，越小安全性越高**

## 步骤5. 保存并关闭该文件。

使用以下命令重新启动fail2ban

```
sudo systemctl restart fail2ban
```

# 二、fail2ban的测试及关闭服务方法

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

# 更多相关知识请参考

仓库地址：[https://github.com/fail2ban/fail2ban](https://github.com/fail2ban/fail2ban)

项目主页：[https://www.fail2ban.org/wiki/index.php/Main_Page](https://www.fail2ban.org/wiki/index.php/Main_Page)

AWS博客介绍：[https://aws.amazon.com/cn/blogs/china/open-source-tool-to-protect-ec2-instances-fail2ban](https://aws.amazon.com/cn/blogs/china/open-source-tool-to-protect-ec2-instances-fail2ban)
