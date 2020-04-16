# 文件备份工具

* 使用工具

  * watchdog 监测文件变化

  * configparser 读取配置文件内容

    * 配置文件内容

      ```
      [DEFAULT]
      ServerAliveInterval = 45
      Compression = yes
      CompressionLevel = 9
      ForwardX11 = yes
        
      [bitbucket.org]
      User = Atlan
        
      [topsecret.server.com]
      Port = 50022
      ForwardX11 = no
      ```

    * 使用

      ```
      import configparser #引入模块
      config = configparser.ConfigParser()    #类中一个方法 #实例化一个对象
      
      config["DEFAULT"] = {'ServerAliveInterval': '45',
                            'Compression': 'yes',
                           'CompressionLevel': '9',
                           'ForwardX11':'yes'
                           }	#类似于操作字典的形式
      
      //读取
      config.read('example.ini')
      print(config.sections())        #   ['bitbucket.org', 'topsecret.server.com']
      print(config['bitbucket.org']["user"])  # Atlan
      # items 得到section的所有键值对
      value = config.items("driver")
      print(value)
      db_options = cf.options("db")
      print db_options    #['db_host', 'db_port', 'db_user', 'db_pass']
      //修改
      config.add_section('yuan')  #添加section
      config.remove_section('bitbucket.org') #删除section
      config.remove_option('topsecret.server.com',"forwardx11") #删除一个配置想
      
      config.set('topsecret.server.com','k1','11111')
      config.set('yuan','k2','22222')
      
      with open('new2.ini','w') as f:
           config.write(f)
      ```

      

  * apscheduler 定时任务 https://mp.weixin.qq.com/s/TTUFQRQ_DiKktJ5-J8O8Pg

    * 安装

      > pip install apscheduler

    * 基本概念

      * 触发器（triggers）：
      * 作业存储器（job stores）：
      * 执行器（executors）：
      * 调度器（schedulers）：

    * 使用

      ```
      #间隔性任务
      from datetime import datetime #打印时间用
      import os #判断操作系统类型
      from apscheduler.schedulers.blocking import BlockingScheduler
      
      def tick():
          print('Tick! The time is: %s' % datetime.now())
      
      if __name__ == '__main__':
          scheduler = BlockingScheduler()
          #触发器为 interval，每隔 3 秒执行一次，另外的触发器为 date，cron。date 按特定时间点触发，cron 则按固定的时间间隔触发
          scheduler.add_job(tick, 'interval', seconds=3)
          print('Press Ctrl+{0} to exit'.format('Break' if os.name == 'nt' else 'C    '))
      
      try:
          scheduler.start()
      except (KeyboardInterrupt, SystemExit):
          pass
          
      # cron 任务
      from datetime import datetime
      import os
      from apscheduler.schedulers.blocking import BlockingScheduler
      
      def tick():
          print('Tick! The time is: %s' % datetime.now())
      
      if __name__ == '__main__':
          scheduler = BlockingScheduler()
          #hour =19 ,minute =23 这里表示每天的19：23 分执行任务。这里可以填写数字，也可以填写字符串
          scheduler.add_job(tick, 'cron', hour=19,minute=23)
          print('Press Ctrl+{0} to exit'.format('Break' if os.name == 'nt' else 'C    '))
      
      try:
      	scheduler.start()
      except (KeyboardInterrupt, SystemExit):
      	pass
      	
      hour =19 , minute =23
      hour ='19', minute ='23'
      minute = '*/3' 表示每 5 分钟执行一次
      hour ='19-21', minute= '23' 表示 19:23、 20:23、 21:23 各执行一次任务
      
      ```

      

  * ftplib ftp文件操作

    ```
    ftp=FTP() #设置变量
    ftp.set_debuglevel(2) #打开调试级别2，显示详细信息
    ftp.connect(“IP”,“port”) #连接的ftp sever和端口
    ftp.login(“user”,“password”)#连接的用户名，密码
    print ftp.getwelcome() #打印出欢迎信息
    ftp.cmd(“xxx/xxx”) #更改远程目录
    bufsize=1024 #设置的缓冲区大小
    filename=“filename.txt” #需要下载的文件
    file_handle=open(filename,“wb”).write #以写模式在本地打开文件
    ftp.retrbinaly(“RETR filename.txt”,file_handle,bufsize) #接收服务器上文件并写入本地文件
    ftp.set_debuglevel(0) #关闭调试模式
    ftp.quit #退出ftp
    ftp相关命令操作
    ftp.cwd(pathname) #设置FTP当前操作的路径
    ftp.dir() #显示目录下文件信息
    ftp.nlst() #获取目录下的文件
    ftp.mkd(pathname) #新建远程目录
    ftp.pwd() #返回当前所在位置
    ftp.rmd(dirname) #删除远程目录
    ftp.delete(filename) #删除远程文件
    ftp.rename(fromname, toname)#将fromname修改名称为toname。
    ftp.storbinaly(“STOR filename.txt”,file_handel,bufsize) #上传目标文件
    ftp.retrbinary(“RETR filename.txt”,file_handel,bufsize)#下载FTP文件
    
    ```
    
    

  * pyinstaller python程序打包

* 类说明

  * 配置文件内容
  
    ```
    [local]
    localdir = E:/ftp
    
    [ftp]
    host = 192.168.1.11
    port = 21
    user = ftpuser
    password = ftpuser
    ftppath = back
    ```
    
  * ftp工具类
  
    ```
    from ftplib import FTP
    
    class FtpUtil:
        def __init__(self, ftpconfig):
            self.config = self.converter(ftpconfig)
            self.ftp = FTP()
            self.ftp.set_debuglevel(2) #打开调试级别2，显示详细信息
        def login(self):
            self.ftp.connect(self.config['host'], int(self.config['port']))
            self.ftp.login(self.config['user'], self.config['password'])
            print(self.ftp.getwelcome()) #打印出欢迎信息
        def upFile(self, filepath):
    
            fp = open(filepath,'rb')
    
            cmd = 'STOR %s/%s' % (self.config['ftppath'],self.getFileNameByPath(filepath)[0])
            print(cmd)
            return self.ftp.storbinary(cmd, fp)
        #将配置文件读出的[(,),(,),(,)] 转换为dict
        def converter(self, source):
            result = {}
            for element in source:
                result[element[0]] = element[1]
            return result
        # 根据文件路径获取文件名
        def getFileNameByPath(self, filepath):
            if '/' in filepath:
                strlist = filepath.split('/')
                return strlist[-1:]
            if '\\'  in filepath:
                strlist = filepath.split('\\')
                return strlist[-1:]
    ```
    
  * 文件监测类
  
    ```
  
    ```
    
    
  
* 一些基础知识

  * 字符串

    ```
    1.字符串截取
    str = '12345678'
    print str[0:1] # 输出str位置0开始到位置1以前的字符
    print str[1:6] # 输出str位置1开始到位置6以前的字符
    str = '0000' + str(num)	# 合并字符串
    print str[-5:]		# 输出字符串右5位
    2.字符串替换 变量.replace("被替换的内容"，"替换后的内容"[，次数])
    str = 'akakak'
    str = str.replace('k',' 8')	# 将字符串里的k全部替换为8
    3.字符串查找
    str = 'a,hello'
    print str.find('hello')	# 在字符串str里查找字符串hello 输出结果2
    4.字符分割
    str = 'a,b,c,d'
    strlist = str.split(',')
    5.字符串包含
    str in strs 
    str1.find(str2)>=0
    6.转换
    int(x [,base ])         将x转换为一个整数    
    long(x [,base ])        将x转换为一个长整数    
    float(x )               将x转换到一个浮点数    
    complex(real [,imag ])  创建一个复数    
    str(x )                 将对象 x 转换为字符串    
    repr(x )                将对象 x 转换为表达式字符串    
    eval(str )              用来计算在字符串中的有效Python表达式,并返回一个对象    
    tuple(s )               将序列 s 转换为一个元组    
    list(s )                将序列 s 转换为一个列表    
    chr(x )                 将一个整数转换为一个字符    
    unichr(x )              将一个整数转换为Unicode字符    
    ord(x )                 将一个字符转换为它的整数值    
    hex(x )                 将一个整数转换为一个十六进制字符串    
    oct(x )                 将一个整数转换为一个八进制字符串   
    ```

  * 字典

    ```
    //添加字典元素
    aa = {'人才':60,'英语':'english','adress':'here'}
    print(aa) # {'人才': 60, '英语': 'english', 'adress': 'here'}
    #添加方法一：根据键值对添加
    aa['价格'] = 100
    print(aa) # {'人才': 60, '英语': 'english', 'adress': 'here', '价格': 100}
    #添加方法二：使用update方法添加
    xx = {'hhh':'gogogo'}
    aa.update(xx)
    print(aa) # {'人才': 60, '英语': 'english', 'adress': 'here', '价格': 100, 'hhh': 'gogogo'}
    
    //删除字典元素
    # 删除方法一：使用del函数
    del[aa['adress']] 或者 del aa['adress']
    print(aa) # {'人才': 60, '英语': 'english', '价格': 100, 'hhh': 'gogogo'}
    #删除方法二：使用pop函数，并返回值
    vv = aa.pop('人才')
    print(vv) # 60
    print(aa) # {'英语': 'english', '价格': 100, 'hhh': 'gogogo'}
    # clear方法，删除所有
    aa.clear()
    print(aa) # {}，为空
    del aa #删除字典
    
    //内置函数
    cmp(dict1, dict2)  #比较两个字典元素。
    len(dict)              #计算字典元素个数，即键的总数。
    str(dict)              #输出字典可打印的字符串表示。
    type(variable)     #返回输入的变量类型，如果变量是字典就返回字典类型。  
    
    
    //内置方法
    radiansdict.clear()    #删除字典内所有元素
    radiansdict.copy()    #返回一个字典的浅复制
    radiansdict.fromkeys()    #创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值
    radiansdict.get(key, default=None)    #返回指定键的值，如果值不在字典中返回default值
    radiansdict.has_key(key)    #如果键在字典dict里返回true，否则返回false
    radiansdict.items()    #以列表返回可遍历的(键, 值) 元组数组
    radiansdict.keys()    #以列表返回一个字典所有的键
    radiansdict.setdefault(key, default=None)    #和get()类似, 但如果键不已经存在于字典中，将会添加键并将值设为default
    radiansdict.update(dict2)    #把字典dict2的键/值对更新到dict里
    radiansdict.values()    #以列表返回字典中的所有值
    ```

  * 线程相关

    * Timer:定时调用函数
  
        ```
        from threading import Timer
        t = Timer(interval, function, args=None, kwargs=None)
        # interval 设置的时间(s) 
        # function 要执行的任务
        # args，kwargs 传入的参数

        t.start()  # 开启定时器
        t.cancel()  # 取消定时器
        ```
  
    
  
  * 中文乱码
  
    > 在 setting.json文件中输入如下代码，保存后运行即可 
    >
    > "code-runner.executorMap": { "python": "set PYTHONIOENCODING=utf-8 && python -u", }