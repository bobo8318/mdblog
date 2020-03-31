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

* 修改远程端口批处理

  ```
  @echo off 
  
  color f0 
  
  echo 修改远程桌面3389端口(支持Windows 2003 2008 2008R2 2012 2012R2 7 8 10 )
  
  echo 自动添加防火墙规则
  
  echo %date%   %time%
  
  echo    ARK set /p c= 请输入新的端口:
  
  if "%c%"=="" goto end
  
  goto edit:
  
  edit 
  
  netsh advfirewall firewall add rule name="Remote PortNumber" dir=in action=allow protocol=TCP localport="%c%"
  
  netsh advfirewall firewall add rule name="Remote PortNumber" dir=in action=allow protocol=TCP localport="%c%"
  
  reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Wds\rdpwd\Tds\tcp" /v "PortNumber" /t REG_DWORD /d "%c%" /f 
  
  reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v "PortNumber" /t REG_DWORD /d "%c%" /f 
  
  echo 修改成功
  
  echo 重启后生效，按任意键重启
  
  pause 
  
  shutdown /r /t 0
  
  exit
  
  :end
  
  echo 修改失败
  
  pause
  ```

* 批处理命令相关内容

    * 一般命令
    
        > @echo off //表示接下来的命令中（不包括本命令），只打印执行结果，不打印命令本身
        >
        > @echo on //表示接下来的命令中（不包括本命令），执行命令前会先把命令打印出来
        >
        > echo %cd%  显示当前路径
        >
        > 
        
    * 一个bat运行其他程序
    
        > start a.bat
        >
        > start "title" "D:\Software\IntelliJ IDEA 2018.3.4\bin\idea64.exe"
        
    * 延迟执行命令
    
        > ping [127.0.0.1](https://www.baidu.com/s?wd=127.0.0.1&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao) -n 3 >nul 利用ping命令 时间大约为 3 - 1 秒