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

  * 后台运行java程序

  	> nohup java -jar xx.jar >/dev/null  & 
    >
    >  \>/dev/null  的作用是输出到空洞  \>/xxx/yyy.out 可以输出到文件
    >
    >  & 代表在后台运行 
    >
    >  nohup 意思是不挂断运行命令,当账户退出或终端关闭时,程序仍然运行， 缺省情况下该作业的所有输出被重定向到nohup.out的文件中 
    >
    > //关闭后台程序
    >
    >  ps aux 查看后台运行程序
    >
    >   kill -9 PID 结束程序
    
  * 环境变量设置
  
    > sudo vi /etc/profile
    > export BASE_PATH = /usr/local/bin
    > export PATH=$PATH:$BASE_PATH 
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
    > firewall-cmd --reload //重新加载防火墙策略
    >
    > netstat -ntlp
    > 或：firewall-cmd --list-ports //查看端口开放效果
  
* 查看端口占用情况
  
  
  > netstat -lnp|grep 8080 
  > netstat -antup |grep 2711 // 通过进程查看端口
  > (yum -y install net-tools)
  > netstat -antup |grep 2711 // 通过进程查看端口


* 进程操作
  > ps 1777 //查看进程信息
  > kill -9 [PID]  #-9 表示强迫进程立即停止
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

* ubuntu

  * ubuntu 修改 ssh默认端口号
  
    ```
    Linux中SSH默认端口为22，为了安全考虑，我们有必要对22端口进行修改，现修改端口为60000；
    
    修改方法如下：
    在/etc/ssh/sshd_config中找到Port 22，将其修改为60000,或使用/usr/sbin/sshd -p 60000指定端口。
    
    如果用户想让22和60000端口同时开放，只需在/etc/ssh/sshd_config增加一行内容如下：
    [root@localhost /]# vi /etc/ssh/sshd_config
    Port 22
    Port 60000
    保存并退出
    [root@localhost /]#service ssh restart
    ```
  
    
  
* mariadb install(2020-04-16) https://www.cnblogs.com/yhongji/p/9783065.html

  > yum install mariadb-server
  >
  > systemctl start mariadb  # 开启服务
  > systemctl enable mariadb  # 设置为开机自启动服务
  > mysql_secure_installation #首次安装需要进行数据库的配置，命令都和mysql的一样
  
  * init set
  
    ```
    Enter current password for root (enter for none):  # 输入数据库超级管理员root的密码(注意不是系统root的密码)，第一次进入还没有设置密码则直接回车
    
    Set root password? [Y/n]  # 设置密码，y
    
    New password:  # 新密码
    Re-enter new password:  # 再次输入密码
    
    Remove anonymous users? [Y/n]  # 移除匿名用户， y
    
    Disallow root login remotely? [Y/n]  # 拒绝root远程登录，n，不管y/n，都会拒绝root远程登录
    
    Remove test database and access to it? [Y/n]  # 删除test数据库，y：删除。n：不删除，数据库中会有一个test数据库，一般不需要
    
    Reload privilege tables now? [Y/n]  # 重新加载权限表，y。或者重启服务也许
    ```
  
  * firewall set
  
    ```
    [root@mini ~]# firewall-cmd --query-port=3306/tcp  # 查看3306端口是否开启
    no
    [root@mini ~]# firewall-cmd --zone=public --add-port=3306/tcp --permanent  # 开启3306端口
    success
    [root@mini ~]# firewall-cmd --reload  # 重启防火墙
    success
    [root@mini ~]# firewall-cmd --query-port=3306/tcp  # 查看3306端口是否开启
    yes
    ```
  
  * char set
  
    ```
    1. /etc/my.cnf 文件 在  [mysqld]  标签下添加
    init_connect='SET collation_connection = utf8_unicode_ci'
    init_connect='SET NAMES utf8'
    character-set-server=utf8
    collation-server=utf8_unicode_ci
    skip-character-set-client-handshake
    
    2. /etc/my.cnf.d/client.cnf 文件 在  [client]  标签下添加
    default-character-set=utf8
    
    3.etc/my.cnf.d/mysql-clients.cnf  文件 在  [mysql]  标签下添加
    default-character-set=utf8
    
    4.restart service
    systemctl restart mariadb
    ```
  
    
  
  * remote connect
  
    ```
    use mysql;
    select host, user from user;
    update user set host='%' where host='mini';
    flush privileges;
    ```
  
    

* Disk 

  *  查看磁盘使用率

    > df -h

  * find local docker dir

    > sudo docker info | grep "Docker Root Dir"

  * move docker file

    > service docker stop
    >
    > mv /var/libdocker /data/docker
    >
    > ln -s /data/docker /var/lib/docker

  * check dir space

    > sudo du -h -x --max-depth=1