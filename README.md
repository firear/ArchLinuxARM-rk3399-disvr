# 简介
- 本项目用于每天自动生成 **rk3399 disvr** 的 **ArchLinuxARM** **aarch64** 系统镜像


 ## 下载地址


 ## 安装了以下软件包及其依赖

  ```
archlinuxarm-keyring base dhcpcd dialog net-tools netctl openssh vi which
  ```
  

 ## 启用了以下服务

  ```
  sshd systemd-networkd systemd-resolved systemd-timesyncd
  ```


  ### IMG文件的额外订制
  
  添加并启用了 **resize2fs_once.service**
  
  ```
  [Unit]
  Description=Resize the root filesystem to fill partition

  [Service]
  Type=oneshot
  ExecStart=/usr/local/bin/growpart /dev/mmcblk0 2 ; /usr/sbin/resize2fs /dev/mmcblk0p2
  ExecStartPost=/usr/bin/systemctl disable resize2fs_once.service ; /usr/bin/rm -rf /etc/systemd/system/resize2fs_once.service /usr/local/bin/growpart

  [Install]
  WantedBy=multi-user.target
  ```
  
  该文件会将 **root** 分区扩展至整张sd卡并在完成后将自身删除
  
  添加了来自 **cloud-guest-utils** 的 **growpart** ，该文件在首次开机时被 **resize2fs_once.service** 使用后删除
 
 ## 使用方式

  **root** 的密码是 ```root```
  
  **alarm** 的密码是 ```alarm```
  
  默认没有安装 **sudo** ，所以通过 **ssh** 登录系统后需要 ```su``` 来获得 **root** 权限

