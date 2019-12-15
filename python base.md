title:python base
date: 2019-11-9
Category: python
Tags: python
Authors: openui
Summary:python base

* 设置位数

  > set CONDA_FORCE_32BIT=1是切换到32位；
  >
  > set CONDA_FORCE_32BIT= 是切换到64位

* create env

  > conda create --name python36 python=3.6
  > conda create -n python2 python=2.7

  * 镜像设置

    * conda

      > conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 
      >
      > conda config --set show_channel_urls yes 

    * pip

      > //临时使用
      >
      > pip install -i https://pypi.tuna.tsinghua.edu.cn/simple numpy 
      >
      > // C:\Users\xx\pip，新建文件pip.ini 内容如下：
      >
      > [global] 
      >
      > index-url = https://pypi.tuna.tsinghua.edu.cn/simple 

  * use env

    > //win
    > activate env_name
    > // linux & mac
    > source activate env_name

  * exit env

    > //win 
    > deactivate
    > //linux & mac
    > source deactivate

  * list env

    > conda env list

  * remove env

    > conda remove --name python36 --all
    > conda env remove -n python36

  * install package

    > conda install package_name
    > conda install numpy=1.14

  * remove package

    > conda remove package_name

  * update package

    > conda update package_name
    
  * 导入导出依赖

    * conda

      >  conda env export > environment.yaml  
      >
      >  conda env update -f=/path/to/environment.yml  

    * pip

      >  pip freeze > environment.txt   
      >
      >  pip install -r C:\Users\Microstrong\enviroment.txt  

* beautifulsoup

  > conda install beautifulsoup4
  > from bs4 import BeautifulSoup

* 模块

  ```
  .
  └── mypackage
      ├── __init__.py  #导入包时会执行这里的代码
      ├── subpackage_1
      │   ├── test11.py
      │   └── test12.py
      ├── subpackage_2
      │   ├── test21.py
      │   └── test22.py
      └── subpackage_3
          ├── test31.py
          └── test32.py
  ```
  
  > from mypackage.subpackage_1 import test11

* 项目打包发布

  > conda install  pyinstaller
  >
  > pyinstaller -F 文件名.py 
  >
  > -F : 打包成单个可执行文件
  > -w : 打包之后运行程序,只有窗口不显示命令行
  > -c : 打包之后运行程序,显示命令行

* 执行系统命令

  >  os.system(cmd): 返回值是脚本的退出状态码，只会有0(成功),1,2 
  >  os.popen(cmd): 返回脚本执行的输出内容作为返回值 
  >
  >  retcode = subprocess.call("cd /data/xxx-salt/ && git pull", shell=True)#创建子进程执行外部程序
  >
  >  
  >
  >   shell=True参数会让subprocess.call接受字符串类型的变量作为命令，并调用shell去执行这个字符串，当shell=False是，subprocess.call只接受数组变量作为命令，并将数组的第一个元素作为命令，剩下的全部作为该命令的参数。 
  >
  >  
  >
  >  md5_value =os.popen('md5sum /root/all.sql')
  >  print(md5_value.read().split()[0])

* 字符串：

  > if str1 in str2:
  >
  > 　　包含的话，True
  >
  > if str1.find(str2)>=0:
  >
  > 　　包含的话，返回第一次出现的位置，没有的话为负数
  >
  > 
  >
  > z = "{0}{1}".format(x, y) 
  > z = "%s%s" % (x, y) 
  >
  > //字符串索引
  >
  > word[:2]# 前两个字符
  > word[2:]# 除前两个字符串外的部分
  >
  > //字符串替换
  >
  > str.replace(old, new[, max])

* python获取当前时间的用法

  >  import datetime 
  >
  >  now_time = datetime.datetime.now() 
  >
  >  “2016-09-21”：datetime.datetime.now().strftime('%Y-%m-%d') 

* 常用命令

  >  os.chdir () # 改变当前工作目录
  >
  >   os.getcwd()  #获取当前工作目录

* 读取配置文件

  
  > //config.ini
  > 
  > [Path]
  > 
  > path = G:\test\openui_ui\content
  
  
  
  
  > import configparser
  >
  > cf = configparser.ConfigParser()
  > cf.read("E:\Crawler\config.ini")  # 读取配置文件，如果写文件的绝对路径，就可以不用os模块
  >
  > secs = cf.sections()  # 获取文件中所有的section(一个配置文件中可以有多个配置，如数据库相关的配置，邮箱相关的配置，每个section由[]包裹，即[section])，并以列表的形式返回
  > print(secs)
  >
  > options = cf.options("Mysql-Database")  # 获取某个section名为Mysql-Database所对应的键
  > print(options)
  >
  > items = cf.items("Mysql-Database")  # 获取section名为Mysql-Database所对应的全部键值对
  > print(items)
  >
  > host = cf.get("Mysql-Database", "host")  # 获取[Mysql-Database]中host对应的值
  > print(host)
  
* python模块之codecs：codecs模块提供一个open方法，三个参数encoding, errors, buffering，这三个参数都是可选参数，但是对于应用来说，需要明确指定encoding的值，而errors和buffering使用默认值即 可

  > import codecs
  >
  > #从文件读取数据
  >
  > data = codecs.open("2.txt", encoding="UTF-8")
  >
  > #一行一行读取数据
  >
  > data1 = data.readline(）
  >
  > print(data1)
  >
  > #读取完数据要把数据对象进行关闭，从内存里面释放出来
  >
  > data.close()

* 定时任务

  * 循环sleep方式

      ```
      from datetime import datetime
      import time
      # 每n秒执行一次
      def timer(n):
          while True:
              print(datetime.now().strftime("%Y-%m-%d  %H:%M:%S"))
              time.sleep(n)

      timer(5)
      ```

  * theading模块中的timer

    ```
    from datetime import datetime
    from threading import Timer
  	# 打印时间函数
    def prinTime(inc):
        print(datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
        t = Timer(inc, printTime,(inc,))
        t.start()
  
    printTime(2)
    ```
  
  * 使用sched模块
  
      ```
      import sched
      import time
      from datetime import datetime
      # 初始化sched模块的scheduler类
      # 第一个参数是一个可以返回时间戳的函数，第二参数可以在定时未到达之前阻塞
      schdule = sched.scheduler(time.time, time.sleep)
      # 被周期性调度触发函数
      def printTime(inc):
          print(datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
          schedule.enter(inc, 0, printTime, (inc,))
      # 默认参数60s
      def main(inc=60):
          # enter四个参数分别为：间隔事件,优先级（用于同时到达两个事件同时执行的顺序），被调度触发的函数
          # 给该触发器函数的参数（tuple形式）
          schedule.enter(0, 0, pirntTime, (inc,))
          schedule.run()
      # 5秒输出一次
      main(5)
      ```
  
  *  APScheduler定时框架
  
  	> pip install APScheduler
  	>
  	> https://www.jianshu.com/p/403bcb57e5c2

