title:docker 下部署 gitlab
date: 2019-9-22
Category: 工具
Tags: docker,git,gitlab
Authors: openui
Summary: docker 下部署 gitlab

### docker 下部署 gitlab

* 下载镜像

  > docker pull gitlab/gitlab-ce

* 运行镜像

  > ```csharp
  >  docker run -d  -p 443:443 -p 80:80 -p 222:22 --name gitlab --restart always -v /home/gitlab/config:/etc/gitlab -v /home/gitlab/logs:/var/log/gitlab -v /home/gitlab/data:/var/opt/gitlab gitlab/gitlab-ce
  > ```

* 配置

  > ```ruby
  > vim /home/gitlab/config/gitlab.rb
  > 
  > # 配置http协议所使用的访问地址,不加端口号默认为80
  > external_url 'http://192.168.199.231'
  > 
  > # 配置ssh协议所使用的访问地址和端口
  > gitlab_rails['gitlab_ssh_host'] = '192.168.199.231'
  > gitlab_rails['gitlab_shell_ssh_port'] = 222 # 此端口是run时22端口映射的222端口
  > 
  > docker restart gitlab
  > ```
  
* 使用

  * 客户端配置ssh
  
    * windows
  
      > //设置用户信息
      >
      > git config --global [user.name](http://user.name) "hanzichi" //给自己起个用户名
      > git config --global user.email ["abc@gmail.com](http://mailto:"abc@gmail.com)" //填写自己的邮箱
      >
      > //生成秘钥
      >
      >  ssh-keygen -t rsa -C "[yourEmail@example.com](https://link.jianshu.com/?t=mailto:yourEmail@example.com)"
  
  * 本地上传仓库
  
    > git init
    >
    > git remote add origin ****
    >
    > git add .
    >
    > git commit -m "first init"
    >
    > git push -u origin master
    
  * 下载仓库
  
    >git clone git@ip:test/website.git
    >
    >cd website
    >
    >touch README.md
    >
    >git add README.md
    >
    >git commit -m "add readme"
    >
    >git push -u origin master
    
  * 已有仓库
  
    > git remote rename origin old-origin
    >
    > git remote add origin ****
    >
    > git push -u origin  --all
    >
    > git push -u origin -- tags
    
  * 每日定时（win）
  
    > //bat 文件内容
    >
    > @echo off
    > @title bat 交互执行git命令
    > D:
    > cd D:/git/test
    > git add .
    > git commit -m %date:~0,4%年%date:~5,2%月%date:~8,2%日
    >
    > git push -u origin master
    >
    > 加入到计划任务里即可
  
* 遇到的问题

  * external_url设置问题：不能带端口
  
  * Whoops, GitLab is taking too much time to respond：比较耗内存 需要多等会
  
    > free -m  查看内存使用情况 如果一直在减少证明还在开启中
  
  * 22端口占用：系统默认22端口被ssh占用，需要释放出来。
  
    * 修改ssh端口
  
      > semanage port -l|grep ssh //查看端口使用情况
      >
      > vim /etc/ssh/sshd_config  //修改配置文件 注意 是sshd 不是ssh
      >
      > 把其中的#Port 22 修改
      >
      > semanage port -a -t ssh_port_t -p tcp 12345  //给SELinux增加设置的端口
      >
      > systemctl restart sshd.service //重启服务
  
  * The file will have its original line endings in your working directory.
  
    > git config --global core.autocrlf false
    
  * 已运行容器修改端口
  
    > 1、获得容器IP
    >
    > docker inspect `container_name` | grep IPAddress
    >
    > 2、iptable转发端口
    >
    > iptables -t nat -A  DOCKER -p tcp --dport 60000 -j DNAT --to-destination 172.17.0.2:22
    >
    > 客户端需要在～/.ssh/config 文件中添加 Host 14.152.10.7 Port 60000
    >
    > 然后需要重新生成秘要上传
