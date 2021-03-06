title:nginx 使用记录
date: 2019-9-22
Category: 工具
Tags: 工具,nginx,linux
Authors: openui
Summary: nginx 使用记录

###  windows 下 nginx 使用

* 下载地址：http://nginx.org/en/download.html

* 运行命令

  > start nginx //运行
  >
  > nginx -t 查看配置状态
  >
  > nginx -s stop/quiet 快速/有序 停止
  >
  > nginx -s reload 重载配置
  >
  > nginx -h 显示帮助信息

* 网站配置

* win下打包为服务

  > Windows Service Wrapper 小工具 下载地址如下：
  >
  > http://repo.jenkins-ci.org/releases/com/sun/winsw/winsw/1.18/winsw-1.18-bin.exe
  >
  > 下载后放在nginx目录下，并修改名字为nginx-service.exe
  > 创建配置文件nginx-service.exe.config 和 nginx-service.xml
  >  nginx-service.exe install  安装服务

  * nginx-service.xml的内容如下：

  > <service>
  ><id>nginx</id>
  > <name>Nginx Service</name>
  >   <description>High Performance Nginx Service</description>
  >   <logpath>C:\nginx-1.14.0\logs</logpath>
  >   <log mode="roll-by-size">
  >    <sizeThreshold>10240</sizeThreshold>
  >    <keepFiles>8</keepFiles>
  >    </log>
  >    <executable>C:\nginx-1.14.0\nginx.exe</executable>
  >   <startarguments>-p C:\nginx-1.14.0</startarguments>
  >   <stopexecutable>C:\nginx-1.14.0\nginx.exe</stopexecutable>
  >   <stoparguments>-p C:\nginx-1.14.0 -s stop</stoparguments>
  >   </service>

  * nginx-service.exe.config内容如下：

  > <configuration>
  > <startup>
  >  <supportedRuntime version="v2.0.50727" />
  >    <supportedRuntime version="v4.0" />
  >    </startup>
  >    <runtime>
  >    <generatePublisherEvidence enabled="false"/> 
  >   </runtime>
  >    </configuration>

  cmd命令输入 sc delete 服务名 可以删除这个服务 powershell下不行



### centos下安装使用
* 查看是否已安装过

  > find -name nginx 
  >
  > yum remove nginx //如果已安装需要删除

* 下载

  >   wget http://nginx.org/download/nginx-1.7.4.tar.gz  
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
