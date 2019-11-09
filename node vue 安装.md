### node vue 安装使用

* node安装,下载地址：

  > https://nodejs.org/en/ 
  >
  > //查看版本号 
  >
  > node -v（node版本）
  >
  > npm -v（npm版本）
  >
  > //安装淘宝镜像
  >
  >  npm install -g cnpm --registry=https://registry.npm.taobao.org

* 安装vue webpack

  >  npm install -g webpack
  >
  > npm install -g vue
  >
  > npm install -g vue-cli

* 使用

  >  vue init webpack vue-projectname 
  >
  > 
  >
  >  cnpm install vue-router vue-resource --save  
  >
  > 
  >
  >  npm run dev //运行项目

* 常用命令

  >  npm update vue-cli 
  >
  >  npm view vue-cli 

* 问题

  * 无法加载文件 C:\Users\hp\AppData\Roaming\npm\cnpm.ps1，因为在此系统上禁止运行脚本。
  
    >  powershell 运行：set-ExecutionPolicy RemoteSigned 