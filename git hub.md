title: github windows下安装使用
date: 2018-05-28
Category: git
Tags: git
Authors: openui
Summary: github windows下安装使用

### 1.git bash 安装
[下载gitbash](https://git-scm.com/download/win)<br>
官网地址：https://git-scm.com/downloads
### 2.ssh 生成(windows下)
* 设置用户信息
>$ git config --global user.name "hanzichi" //给自己起个用户名<br>
$ git config --global user.email  "abc@gmail.com" //填写自己的邮箱
* 生成秘钥
> ssh-keygen -t rsa -C "abc@163.com"  

最后得到了两个文件：id_rsa和id_rsa.pub 复制id_rsa.pub文件内容 在github中新建ssh key 添加保存
* 测试命令
> ssh git@github.com 
* 使用ssh
    * 查看当前url
    >Git remote -v //默认使用的是https
    使用类似 git@github.com:someaccount/someproject.git的sshurl 在github网站上可以获取

    * 设置ssh地址
    > git remote set-url origin git@github.com:someaccount/someproject.git
### 3.使用命令
* git clone **(项目地址)
克隆一个git项目到本地,将git项目拉取到本地
* git status 
查看文件状态,列出当前目录没有被git管理，以及被修改过还未提交的文件
* git add *
将我们提交的文件添加到索引库中（添加到缓冲区），*可以是路径也可以是.符号，* git add . 代表将当前目录下的所有文件都添加到索引库中,如果指定路径则代表将制定路径的文件添加到索引库中。
*  git commit -m "备注"
将文件推送到本地仓库中,-m 后可以填写此次提交的备注如git commit -m "提交删除功能代码"，那么在git项目中的提交记录里面就能看见你的推送备注。这一步仅仅是放在缓冲区中，还未真正提交代码
*  git push origin 分支名
这一步才是推送代码推送时需要跟分支名，表示需要将代码推送至某个分支.如git *  push origin dev表示你要讲代码推送至dev分支。
*  git pull
更新当前分支的代码,获取最新的代码
*  git checkout 分支名
切换分支
*  git merge 分支名
当前分支合并其他分支
所以一般的使用简易流程 git add ， git commit -m "", git push origin 。 当然如果远端有代码更新的情况需要git pull更新一下，中间也可以使用git status 查看不同时期的状态

### 常用流程

```
git pull
git add .
git commit -m,message
git push
```