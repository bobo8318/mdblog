* 查看是否安装过jdk

  >  **rpm -qa | grep java** 
  >
  >  **rpm -e xxx --nodeps** // 卸载

* 解压

  >  tar -xvf  jdk-8u231-linux-x64.tar.gz

* 修改环境变量

  >  vi /etc/profile
  >
  > 在最底行添加如下：
  >
  > JAVA_HOME=/opt/java/jdk1.8.0_231
  >
  > CLASSPATH=.:$JAVA_HOME/lib.tools.jar
  >
  > PATH=$JAVA_HOME/bin:$PATH
  >
  > export JAVA_HOME CLASSPATH PATH
  >
  > //
  >
  >  source /etc/profile
  >
  > java -version