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
    
  * 清除缓存

    > conda clean -p // 没有用的包
    >
    > conda clean -t  //tar

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

* yield

  ```
  1.程序开始执行以后，因为foo函数中有yield关键字，所以foo函数并不会真的执行，而是先得到一个生成器g(相当于一个对象)
  
  2.直到调用next方法，foo函数正式开始执行，先执行foo函数中的print方法，然后进入while循环
  
  3.程序遇到yield关键字，然后把yield想想成return,return了一个4之后，程序停止，并没有执行赋值给res操作，此时next(g)语句执行完成，所以输出的前两行（第一个是while上面的print的结果,第二个是return出的结果）是执行print(next(g))的结果，
  4.程序执行print("*"*20)，输出20个*
  
  5.又开始执行下面的print(next(g)),这个时候和上面那个差不多，不过不同的是，这个时候是从刚才那个next程序停止的地方开始执行的，也就是要执行res的赋值操作，这时候要注意，这个时候赋值操作的右边是没有值的（因为刚才那个是return出去了，并没有给赋值操作的左边传参数），所以这个时候res赋值是None,所以接着下面的输出就是res:None,
  
  6.程序会继续在while里执行，又一次碰到yield,这个时候同样return 出4，然后程序停止，print函数输出的4就是这次return出的4.
  
  
  def foo():
      print("starting...")
      while True:
          res = yield 4
          print("res:",res)
  g = foo()
  print(next(g))
  print("*"*20)
  print(next(g))
  //输出
  starting...
  4
  ********************
  res: None
  4
  
  ```

* 运算符重载

  ```
  class MyClass: #自定义一个类
      def __init__(self, name , age): #定义该类的初始化函数
          self.name = name #将传入的参数值赋值给成员交量
          self.age = age
      def __str__(self): #用于将值转化为字符串形式，等同于 str(obj)
          return "name:"+self.name+";age:"+str(self.age)
     
      __repr__ = __str__ #转化为供解释器读取的形式
     
      def __lt__(self, record): #重载 self<record 运算符
          if self.age < record.age:
              return True
          else:
              return False
     
      def __add__(self, record): #重载 + 号运算符
          return MyClass(self.name, self.age+record.age)
          
  myc = MyClass("Anna", 42) #实例化一个对象 Anna，并为其初始化
  mycl = MyClass("Gary", 23) #实例化一个对象 Gary，并为其初始化
  print(repr(myc)) #格式化对象 myc，
  print(myc) #解释器读取对象 myc，调用 repr
  print (str (myc)) #格式化对象 myc ，输出"name:Anna;age:42"
  print(myc < mycl) #比较 myc<mycl 的结果，输出 False
  print (myc+mycl) #进行两个 MyClass 对象的相加运算，输出 "name:Anna;age:65"
  ```

* 循环

  ```
//enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标.enumerate(sequence, [start=0]) start -- 下标起始位置。
  a = [8, 23, 45, 12, 78]
  for index, value in enumerate(a):
  	print(index , value)
  ```
  
* 判断

  ```
  x = [True, True, False]
  	if any(x):
  	  print '至少一个为真'
  	if all(x):
  	  print '全部为真'
  	if any(x) and not all(x):
  	  print '至少一个为真、一个为假'
  	  
  	  
  // for正常结束会执行else break出去不会执行
  for i in list1:
      if 'nb' in i:
          print("list1 里有nb人:"+i[0:2])
          break
  else:
      print("list1里没有nb人！")
  ```

  

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

