> [!NOTE]
> 文章来源：[hebaodan](https://linux.do/t/topic/181957)

### Serv00重置系统命令

#### 1.更改权限：
```
find ~ -type f -exec chmod 644 {} \; 2>/dev/null
find ~ -type d -exec chmod 755 {} \; 2>/dev/null
```

#### 2.删除文件：
```
find ~ -type f -exec rm -f {} \; 2>/dev/null
```

#### 3.删除空目录：
```
find ~ -type d -empty -exec rmdir {} \; 2>/dev/null
```

#### 4.再次尝试删除剩余的文件和目录：
```
find ~ -exec rm -rf {} \; 2>/dev/null
```

---
#### 删除所有进程命令

```
bash <(curl -Ls https://raw.githubusercontent.com/eooce/sing-box/main/sb_serv00.sh)
```