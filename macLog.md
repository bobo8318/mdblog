###  04.24

* 安装Command Line tools

  > Xcode-select --install

* 安装brew命令

  > 修改etc 下的 hosts文件 在末尾添加
  >
  > 199.232.28.133	raw.githubusercontent.com
  >
  > Run command:
  >
  > /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
  >
  > 更换源：https://www.cnblogs.com/trotl/p/11862796.html
  >
  > 
  >
  > brew uninstall wget
  >
  > brew search /wge*/.  /wge*/是个正则表达式， 需要包含在/中
  >
  > brew list 列出已安装的软件
  >
  > brew update 更新brew
  >
  > brew home 用浏览器打开brew的官方网站
  >
  > brew info 显示软件信息
  >
  > brew deps 显示包依赖

  * 一些问题
    * Error: Another active Homebrew update process is already in progress. Please wait for it to finish or terminate it to continue.

      > rm -rf /usr/local/var/homebrew/locks

    * git报错fatal: the remote end hung up unexpectedly

      > git config --global ssh.postBuffer 1048576000

* install nginx

  > brew install nginx
  >
  > nginx -V 查看nginx版本及安装的本地位置
  >
  > sudo nginx // run nginx
  >
  > sbin/nginx  启动
  >
  > sbin/nginx -s reload 重新加载
  >
  > sbin/nginx -s stop 停止，无日志
  >
  > sbin/nginx -s quit 停止，有日志 
  >
  > 
  >
  > brew services stop nginx
  >
  > brew services restart nginx
  >
  > nginx -t 验证配置文件
  >
  > /usr/local/etc/nginx/nginx.conf 配置文件位置

* install maven

  ```
  download & 
  
  vim ~/.bash_profile
  
  MAVEN_HOME=/Users/light6/JavaFile/apache-maven-3.6.2
  export MAVEN_HOME
  export PATH=$MAVEN_HOME/bin:$PATH
  
  source .bash_profile
  mvn -v
  
  
  http://127.0.0.1:8081/nexus/content/groups/public/ 2
  http://127.0.0.1:8081/repository/maven-public/  3
  ```

  

* vi & vim

  ```
  i 　切换到插入模式，以输入字符。
  x   删除当前光标所在处的字符。
  :   切换到底线命令模式，以在最底一行输入命令。
  
  ENTER(回车键)      　　 换行
  BACK SPACE(退格键) 　　 删除光标前一个字符
  方向键        　　　　　　在文本中移动光标
  HOME/END               　移动光标到行首/行尾
  Page Up/Page Down       上/下翻页
  ESC                    　退出输入模式，切换到命令模式
  
  q 　　退出程序
  w 　　保存文件
  按ESC键可随时退出底线命令模式。
  
  ```

* tar解压与压缩打包命令

  ```
  -c ：建立一个压缩文件的参数指令(create 的意思)；
  -x ：解开一个压缩文件的参数指令！
  -t ：查看 tarfile 里面的文件！
  特别注意，在参数的下达中， c/x/t 仅能存在一个！不可同时存在！
  因为不可能同时压缩与解压缩。
  -z ：是否同时具有 gzip 的属性？亦即是否需要用 gzip 压缩？
  
  范例一：将整个 /etc 目录下的文件全部打包成为 /tmp/etc.tar
  [root@linux ~]# tar -cvf /tmp/etc.tar /etc         <==仅打包，不压缩！
  [root@linux ~]# tar -zcvf /tmp/etc.tar.gz /etc       <==打包后，以 gzip 压缩
  
  范例二：查阅上述 /tmp/etc.tar.gz 文件内有哪些文件？
  [root@linux ~]# tar -ztvf /tmp/etc.tar.gz
  # 由於我们使用 gzip 压缩，所以要查阅该 tar file 内的文件时，
  # 就得要加上 z 这个参数了！这很重要的！
  
  范例三：将 /tmp/etc.tar.gz 文件解压缩在 /usr/local/src 底下
  [root@linux ~]# cd /usr/local/src
  [root@linux src]# tar -zxvf /tmp/etc.tar.gz
  
  
  tar 
  解包：tar xvf FileName.tar
  打包：tar cvf FileName.tar DirName
  （注：tar是打包，不是压缩！）
  ———————————————
  .gz
  解压1：gunzip FileName.gz
  解压2：gzip -d FileName.gz
  压缩：gzip FileName
  
  .tar.gz 和 .tgz
  解压：tar zxvf FileName.tar.gz
  压缩：tar zcvf FileName.tar.gz DirName
  ———————————————
  .bz2
  解压1：bzip2 -d FileName.bz2
  解压2：bunzip2 FileName.bz2
  压缩： bzip2 -z FileName
  
  .tar.bz2
  解压：tar jxvf FileName.tar.bz2
  压缩：tar jcvf FileName.tar.bz2 DirName
  ———————————————
  .bz
  解压1：bzip2 -d FileName.bz
  解压2：bunzip2 FileName.bz
  压缩：未知
  
  .tar.bz
  解压：tar jxvf FileName.tar.bz
  压缩：未知
  ———————————————
  .Z
  解压：uncompress FileName.Z
  压缩：compress FileName
  .tar.Z
  
  解压：tar Zxvf FileName.tar.Z
  压缩：tar Zcvf FileName.tar.Z DirName
  ———————————————
  .zip
  解压：unzip FileName.zip
  压缩：zip FileName.zip DirName
  ———————————————
  .rar
  解压：rar x FileName.rar
  压缩：rar a FileName.rar DirName
  ———————————————
  .lha
  解压：lha -e FileName.lha
  压缩：lha -a FileName.lha FileName
  ———————————————
  .rpm
  解包：rpm2cpio FileName.rpm | cpio -div
  ———————————————
  .deb
  解包：ar p FileName.deb data.tar.gz | tar zxf -
  ———————————————
  .tar .tgz .tar.gz .tar.Z .tar.bz .tar.bz2 .zip .cpio .rpm .deb .slp .arj .rar .ace .lha .lzh .lzx .lzs .arc .sda .sfx .lnx .zoo .cab .kar .cpt .pit .sit .sea
  解压：sEx x FileName.*
  压缩：sEx a FileName.* FileName
  ```

  

* install mariadb

  ```
  brew info mariadb //install
  mysql.server start //run
  mysql.server stop // stop
  sudo mysql_secure_installation // init password
  
  mysql>source d:wcnc_db.sql
  
  ```

* intall nexus

  ```
  //help url
  https://www.cnblogs.com/cangqinglang/p/9640666.html
  https://blog.csdn.net/wyz0923/article/details/101519684
  https://blog.csdn.net/lusyoe/article/details/52821088
  https://www.jianshu.com/p/91a93ebde656 //安装
  
  // down url
  https://help.sonatype.com/repomanager3/download/download-archives---repository-manager-3
  http://download.sonatype.com/nexus/3/nexus-3.19.1-01-mac.tgz
  
  // extra file
  tar zxvf exus-3.19.1-01-mac.tgz
  // run nexus
  cd nexus-3.5.1-02-mac/nexus-3.5.1-02/bin
  ./nexus start
  // url
  http://127.0.0.1:8081/#
  http://127.0.0.1:8081/#admin/repository/repositories:maven-central
  // build index url
  https://repo.maven.apache.org/maven2/.index/
  https://repo.maven.apache.org/maven2/.index/nexus-maven-repository-index.properties
  
  java -jar indexer-cli-5.1.1.jar -u nexus-maven-repository-index.gz -d indexer
  
  
  /Users/openui/Downloads/sonatype-work/nexus3/blobs/default/.index
  
  //npm 
  npm config set registry http://127.0.0.1:8081/nexus/content/groups/npm-group/
  npm config set registry http://127.0.0.1:8081/nexus/content/repositories/npm-proxy/
  npm config set registry http://127.0.0.1:8081/repository/npm-repo-proxy/
  
  ```
  
* 基础 

  > lsof
  >
  > lsof | less
  >
  > lsof -i:3000

* shell

  > echo ‘hello’
  >
  > chmod +x testtest.sh
  >
  > ./testtest.sh
  
* install jdk

  ```
  sudo vim .bash_profile
  export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_191.jdk/Contents/Home
  source .bash_profile
  
  sudo xcode-select --switch /Applications/Xcode-beta.app/Contents/Developer
  ```

  

  * jdk

    ```
    # 运行以下命令会安装 Oracle 提供的 Oracle JDK12
    brew cask install oracle-jdk
     
    # 在2019年5月
    ## 该命令会安装由 Oracle 提供的 OpenJDK12
    brew cask install java
    ## 而该命令则安装由 Oracle 提供的 OpenJDK11
    brew cask install java1
    
    install location:/Library/Java/JavaVirtualMachines
    ```
  

  * Openjdk
```
brew tap AdoptOpenJDK/openjdk //下载库
brew search /adoptopenjdk/  ／／搜素

brew cask install AdoptOpenJDK/openjdk/adoptopenjdk8
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk9
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk10
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk11
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk12
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk
  
```

* Anaconda 安装opencv

  > Brew install opencv3 //python3

* Php

```
mac 自带php
php -v 

Mac 自带 apache
位置：/etc/apache2
运行：sudo /usr/sbin/apachectl start
default_web_location: /Library/WebServer/Documents

常见问题
AH00557: httpd: apr_sockaddr_info_get() failed for My-MacBook-Pro.local
AH00558: httpd: Could not reliably determine the server's fully qualified
domain name, using 127.0.0.1. Set the 'ServerName' directive globally to
suppress this message
https://apple.stackexchange.com/questions/280099/apache-on-macos-sierra-ah00557-httpd-apr-sockaddr-info-get-failed-for-macbo/285445
```

* vscode+