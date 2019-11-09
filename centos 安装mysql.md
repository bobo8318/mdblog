* 检查卸载mariadb-lib


  > #检查
  > [root@imok ~]# rpm -qa|grep mariadb
  > mariadb-libs-5.5.60-1.el7_5.x86_64
  > #卸载
  > [root@imok ~]# rpm -e mariadb-libs-5.5.60-1.el7_5.x86_64 --nodeps

* 下载安装

  >  wget -i -c https://repo.mysql.com/mysql57-community-release-el7-10.noarch.rpm 
  >
  >  yum -y install mysql57-community-release-el7-10.noarch.rpm // 安装 Yum Repository
  >
  >  yum -y install mysql-community-server //安装mysql

* 使用

  >  systemctl start  mysqld.service  启动
  >
  >  systemctl status mysqld.service 
  >
  >  grep "password" /var/log/mysqld.log  查看默认初始密码
  >
  >  mysql -u root -p  登录
  >
  >  ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';  修改密码

* 常见问题

  * 支持中文

    >  vi /etc/my.cnf 
    >
    >  service mysqld restart 
    >
    >  show variables like 'character_set%';