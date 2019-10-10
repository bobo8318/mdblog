title:nginx 使用记录
date: 2019-9-22
Category: 工具
Tags: 工具,nginx
Authors: openui
Summary: nginx 使用记录

###  nginx 使用

* 下载地址：http://nginx.org/en/download.html

* 运行命令

  > start nginx //运行
  >
  > nginx -t 查看配置状态
  >
  > nginx -s stop/quiet 快速/有序 停止

* 网站配置

* win下打包为服务

  > Windows Service Wrapper 小工具 下载地址如下：
  >
  >  http://repo.jenkins-ci.org/releases/com/sun/winsw/winsw/1.18/winsw-1.18-bin.exe
  >
  > 下载后放在nginx目录下，并修改名字为nginx-service.exe
  >
  > 创建配置文件nginx-service.exe.config 和 nginx-service.xml

  > nginx-service.xml的内容如下：
  >
  > <service>
  >   <id>nginx</id>
  >   <name>Nginx Service</name>
  >   <description>High Performance Nginx Service</description>
  >   <logpath>C:\nginx-1.14.0\logs</logpath>
  >   <log mode="roll-by-size">
  >     <sizeThreshold>10240</sizeThreshold>
  >     <keepFiles>8</keepFiles>
  >   </log>
  >   <executable>C:\nginx-1.14.0\nginx.exe</executable>
  >   <startarguments>-p C:\nginx-1.14.0</startarguments>
  >   <stopexecutable>C:\nginx-1.14.0\nginx.exe</stopexecutable>
  >   <stoparguments>-p C:\nginx-1.14.0 -s stop</stoparguments>
  > </service>

  > nginx-service.exe.config内容如下：
  >
  > <configuration>
  >   <startup>
  >     <supportedRuntime version="v2.0.50727" />
  >     <supportedRuntime version="v4.0" />
  >   </startup>
  >   <runtime>
  >     <generatePublisherEvidence enabled="false"/> 
  >   </runtime>
  > </configuration>

  cmd命令输入 sc delete 服务名 可以删除这个服务