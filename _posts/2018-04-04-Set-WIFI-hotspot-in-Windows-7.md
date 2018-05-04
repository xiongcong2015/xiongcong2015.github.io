---
layout: default
title: Windows 7 设置 WIFI 热点
---

# 在 Windows 7 系统上设置 WIFI 热点

```shell
# 以管理员权限设置热点名称和密码
netsh wlan set hostednetwork mode=allow ssid=Dell12345 key=qwertyuiop
```

在网络和共享中心打开本地连接的属性，共享里面选项打开后选择新生成的无线连接


```shell
# 启动热点
netsh wlan start hostednetwork
# 关闭热点
netsh wlan stop hostednetwork
```
