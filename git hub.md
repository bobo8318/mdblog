title: github 安装使用
date: 2018-05-28
Category: git
Tags: git
Authors: openui
Summary: github 下安装使用

### 1.git bash 安装
[下载gitbash](https://git-scm.com/download/win)<br>
官网地址：https://git-scm.com/downloads
### 2.ssh 生成(windows下)
* 设置用户信息
>$ git config --global user.name "hanzichi" //给自己起个用户名<br>
$ git config --global user.email  "abc@gmail.com" //填写自己的邮箱
* 生成秘钥
> ssh-keygen -t rsa -C "abc@163.com"  
>
> // linux 默认路径
>
>  /home/user/.ssh 
>
> //windows默认路径
>
>  C:\Users\Administrator\.ssh 

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

* git commit -m "备注"
  将文件推送到本地仓库中,-m 后可以填写此次提交的备注如git commit -m "提交删除功能代码"，那么在git项目中的提交记录里面就能看见你的推送备注。这一步仅仅是放在缓冲区中，还未真正提交代码

* git push origin 分支名
  这一步才是推送代码推送时需要跟分支名，表示需要将代码推送至某个分支.如git *  push origin dev表示你要讲代码推送至dev分支。

* git pull
  更新当前分支的代码,获取最新的代码

* git checkout 分支名
  切换分支

* git merge 分支名
  当前分支合并其他分支
  所以一般的使用简易流程 git add ， git commit -m "", git push origin 。 当然如果远端有代码更新的情况需要git pull更新一下，中间也可以使用git status 查看不同时期的状态

* git remote show origin 查看远程仓库地址

* git remote set-url origin git@192.168.30.29:chenwei/em-data.com.cn.git 修改远程仓库地址

* git remote add origin "xxx.git" 设置远程仓库地址

  

### 常用流程

```
git pull
git add .
git commit -m,message
git push
```

### .gitignore

> /mtk 过滤整个文件夹
> *.zip 过滤所有.zip文件
> /mtk/do.c 过滤某个具体文件
> !/mtk/one.txt 追踪（不过滤）某个具体文件
>
> 以斜杠“/”开头表示目录；
> 以星号“*”通配多个字符；
> 以问号“?”通配单个字符
> 以方括号“[]”包含单个字符的匹配列表；
> 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录。

* gitignore不起作用

> git rm -r --cached .//删除本地缓存
> git add .
> git commit -m 'update .gitignore'

* crlf转换问题 由于linux和windows换行符不同

  > // 提交时转换为LF，检出时转换为CRLF
  > git config --global core.autocrlf true
  >
  > // 提交时转换为LF，检出时不转换
  > git config --global core.autocrlf input
  >
  > // 提交检出均不转换
  > git config --global core.autocrlf false

* 遇到问题-----git-----You have not concluded your merge (MERGE_HEAD exists) git拉取失败

  > 有2个解决办法:
  > 1.保留你本地的修改
  >
  > git merge --abortgit reset --merge
  > 合并后记得一定要提交这个本地的合并然后在获取线上仓库
  >
  > git pull
  >
  > 2.down下线上代码版本,抛弃本地的修改
  >
  > git fetch --all
  > git reset --hard origin/master
  >
  > git fetch

* 修改远程ssh连接端口

  > 编辑~/ .ssh / config文件。添加如下内容：
  >
  > Host example.com
  >     Port 1234

* 新建分支

  > checkout dev -b

* 合并分支

  * > git merge –no-ff 可以保存你之前的分支历史。能够更好的查看 merge历史，以及branch 状态。
  >
    > git merge 则不会显示 feature，只保留单条分支记录。
  
  * 快进”(无冲突)
  
    > $ git checkout -b dev
    >
    > 
    >
    > $ git checkout master
    >
    > $ git merge dev
    >
    > $ git branch -d dev
  
  * 有冲突
  
    > $ git status 查看冲突文件
    >
    > 修改 后 
    >
    > $ git add .
    >
    > $ git commit -m 'test'
    >
    > $ git branch -d dev
  
* 常见问题

  * git remote set-url origin "xxx.git" 报错 No such remote 'origin'

    > git remote add origin "xxx.git"

  * Updates were rejected because the remote contains work that you do
  
    > push 之前 先 git pull origin master 即可