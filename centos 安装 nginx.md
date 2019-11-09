title:centos安装nginx
date: 2019-11-9
Category: linux
Tags: linux,centos,nginx
Authors: openui
Summary:cengtos下nginx安装

* 查看是否已安装过

  > find -name nginx 
  >
  > yum remove nginx //如果已安装需要删除

* 下载

  >   wget http://nginx.org/download/nginx-1.7.4.tar.gz  
  >
  >  yum -y install wget  //安装wget

* 解压

  >   tar -zxvf nginx-1.7.4.tar.gz   

* 编译安装

  >  yum install gcc-c++ 
  >
  >  yum install pcre pcre-devel 
  >
  >  yum install zlib zlib-devel  
  >
  >  yum install openssl openssl--devel  
  >
  >  // 报./configure: error: C compiler cc is not found错误 执行下面命令
  >
  >  yum -y install gcc gcc-c++ autoconf automake make  
  >
  >  
  >
  >  ./configure --prefix=/opt/nginx    // 编译的时候用来指定程序存放路径 
  >
  >  make
  >
  >  make install
  
* 运行

  > sudo sbin/nginx

* 设置开机启动

  > cd /lib/systemd/system/
  >
  > vi nginx.service
  >
  > //内容如下
  >
  > [Unit]
  > Description=nginx service
  > After=network.target 
  >
  > [Service] 
  > Type=forking 
  > ExecStart=/opt/nginx/sbin/nginx
  > ExecReload=/opt/nginx/sbin/nginx -s reload
  > ExecStop=/opt/nginx/sbin/nginx -s quit
  > PrivateTmp=true 
  >
  > [Install] 
  > WantedBy=multi-user.target
  >
  > //说明
  >
  > [Unit] 服务的说明
  > Description:描述服务
  > After:描述服务类别
  > [Service]服务运行参数的设置
  > Type=forking是后台运行的形式
  > ExecStart为服务的具体运行命令
  > ExecReload为重启命令
  > ExecStop为停止命令
  > PrivateTmp=True表示给服务分配独立的临时空间
  > 注意：[Service]的启动、重启、停止命令全部要求使用绝对路径
  > [Install]运行级别下服务安装的相关设置，可设置为多用户，即系统运行级别为3 
  >
  > // 加入开机启动
  >
  > systemctl enable nginx
  >
  > // 取消开机启动
  >
  > systemctl disable nginx
  > // 常用操作
  > systemctl start nginx.service　         启动nginx服务
  >
  > systemctl stop nginx.service　          停止服务
  >
  > systemctl restart nginx.service　       重新启动服务
  >
  > systemctl list-units --type=service     查看所有已启动的服务
  >
  > systemctl status nginx.service          查看服务当前状态
  >
  > systemctl enable nginx.service          设置开机自启动
  >
  > systemctl disable nginx.service         停止开机自启动



