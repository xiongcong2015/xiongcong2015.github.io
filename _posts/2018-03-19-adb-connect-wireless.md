---
layout: default
title: adb 无线连接调试 Android 设备
---

# adb 无线连接调试 Android 设备
电脑和手机连在同一网络的情况下，先用USB线连接Android设备，然后打开CMD窗口运行如下命令。
```shell
Microsoft Windows [版本 10.0.16299.309]
(c) 2017 Microsoft Corporation。保留所有权利。

C:\Users\bryan>adb devices
List of devices attached
* daemon not running; starting now at tcp:5037
* daemon started successfully
77e15b91        device


C:\Users\bryan>adb tcpip 5555
restarting in TCP mode port: 5555

C:\Users\bryan>adb connect 172.26.226.183
connected to 172.26.226.183:5555

C:\Users\bryan>adb shell
hero2qltechn:/ $ ls
acct               init.msm.usb.configfs.rc   persist
bt_firmware        init.qcom.class_core.sh    postrecovery.do
bugreports         init.qcom.early_boot.sh    preload
cache              init.qcom.factory.rc       proc
config             init.qcom.rc               property_contexts
d                  init.qcom.sensors.sh       publiccert.pem
data               init.qcom.sh               root
default.prop       init.qcom.syspart_fixup.sh sbin
dev                init.qcom.usb.rc           sdcard
dsp                init.qcom.usb.sh           seapp_contexts
efs                init.rc                    sepolicy
etc                init.rilchip.rc            sepolicy_version
file_contexts.bin  init.target.rc             service_contexts
firmware           init.usb.configfs.rc       storage
firmware-modem     init.usb.rc                sys
fstab.qcom         init.wifi.rc               system
init               init.zygote32.rc           tombstones
init.carrier.rc    init.zygote64_32.rc        ueventd.qcom.rc
init.class_main.sh knox_data                  ueventd.rc
init.container.rc  mnt                        vendor
init.environ.rc    oem                        verity_key
init.mdm.sh        persdata
hero2qltechn:/ $
```
