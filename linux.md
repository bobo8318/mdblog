title:linux知识记录
date: 2019-9-22
Category: linux
Tags: linux
Authors: openui
Summary:linux知识记录

### linux

* 常用软件安装

  * firefox

    >  yum -y install firefox 

* centos

  * 环境变量设置

    > sudo vi /etc/profile
    >
    > 
    >
    > export BASE_PATH = /usr/local/bin
    >
    > export PATH=$PATH:$BASE_PATH 
    >
    > 
    >
    > source /etc/profile

  * 开启防火墙及特定端口
  
    > firewall-cmd --state //查看防火墙状态
    >
    > systemctl start firewalld.service //启动防火墙
    >
    > systemctl enable firewalld.service  //设置开机启动
    >
    > systemctl restart firewalld.service  //重启防火墙
    >
    > systemctl is-enabled firewalld.service;echo $? //查看防火墙设置开机自启是否成功
    >
    > // 开启端口
    >
    > firewall-cmd --zone=public --add-port=80/tcp --permanent
    >
    > --zone #作用域
    > --add-port=80/tcp  #添加端口，格式为：端口/通讯协议
    > --permanent   #永久生效，没有此参数重启后失效
    >
    > 
    >
    > firewall-cmd --reload //重新加载防火墙策略
    >
    > 
    >
    > netstat -ntlp
    > 或：firewall-cmd --list-ports //查看端口开放效果
  
  * 查看端口占用情况
  

  > netstat -lnp|grep 8080 
  > netstat -antup |grep 2711 // 通过进程查看端口
  >

  
  * 进程操作
  

  > ps 1777 //查看进程信息
  > kill -9 [PID]  #-9 表示强迫进程立即停止
  >
  > ps -ef|grep redis //知道服务名称

  * 权限
   * Centos7 普通用户加入sudo组
   > whereis sudoers//查找
   > vi /etc/sudoers //编辑
   > root ALL = (ALL) ALL //下面添加需要添加的用户
  
  * centos 网络设置
    > ip addr 查看IP地址
    > vi /etc/sysconfig/network-scripts/ifcfg-eth0  //网卡配置地址文件
    > ONBOOT=yes   #系统启动时是否激活此设备 默认不开启 需要开启一下

  * 常见故障：
  
    * su:鉴定故障
    
      >  sudo passwd root
      > 输入当前用户密码，然后输入设置的root密码

