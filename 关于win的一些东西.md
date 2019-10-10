title:关于winserver的一些记录
date: 2019-9-22
Category: server
Tags: windows,server,sql,iis
Authors: openui
Summary: 关于winserver的一些记录

### 关于IIS的一些东西

* asp

  * IIS7显示ASP的详细错误信息到浏览器
  
    >  // 服务端
    >
    > 网站->ASP->调试属性->将错误发送到浏览器，修改为True
    >
    >  网站-->错误页-->操作-->编辑功能设置，选择“详细错误信息”
    >
    > // 客户端
    >
    > 网站属性页--“主目录”选项卡--“配置” 按钮--“调试” 选项卡
    >
    > 关掉 显示友好的http错误信息 禁止脚本调试

### 关于sql2000的一些东西

* 安装中遇到的问题

  * 安装提示挂起 

    > HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager 删除PendingFileRenameOperations

  * windows 2008 R2 64 系统安装SQL2000 32位数据库

    * 找到\ENTERPRISE\X86\SETUP\setupsql.exe文件 右键属于-兼容模式（勾选兼容性windows 2003 SP1，管理员）
    * sp4补丁 同样设置 SQL2000\SQL2KSP4\x86\setup\setupsql.exe 

* 数据恢复

  * 如果有数据库 _Log 和 _Data 文件 在新数据库新建同样名字的数据库，然后替换掉就可以了

    

* 测试
  
  * telnet 192.168.1.1 1433 测试1433端口是否开启

### 关于操作系统的一些操作

* 查看端口


  > netstat -ano | findstr 9999

* 远程桌面修改端口（默认3389）

    * 注册表(运行-regedit) 修改后重启电脑即可

      > ／／　修改处１
      >
      > HKEY_LOCAL_MACHINE
      >
      > SYSTEM
      >
      > CurrentControlSet
      >
      > Control
      >
      > Terminal Server
      >
      > Wds
      >
      > rdpwd
      >
      > Tds
      >
      > tcp
      >
      > PortNumber 选择10进制　修改端口
      >
      > ／／　修改处２
      >
      > Terminal Server
      >
      > WinStations
      >
      > RDP-Tcp 
      >
      > PortNumber 选择10进制　修改端口