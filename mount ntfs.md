# 挂载ntfs移动硬盘

## 安装包
`apt-get install ntfs-3g`

## 挂载
```
mkdir /media/wind 
mount -t auto /dev/sdc6 /media/wind
```
## 卸载
`umount /media/wind`
