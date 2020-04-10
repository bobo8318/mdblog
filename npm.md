* 升级

  > npm install -g npm
  > npm init -y  生成package.json

* 安装cnpm，输入以下命令：

  > npm install -g cnpm --registry=https://registry.npm.taobao.org

* 安装依赖

  > npm install 
  >
  > cnpm install
  >
  > 
  >
  > npm install module_name -S  即  npm install module_name --save  写入dependencies
  >
  > npm install module_name -D  即  npm install module_name --save-dev 写入devDependencies
  >
  > npm install module_name -g 全局安装(命令行使用)
  >
  > npm install module_name 本地安装(将安装包放在 ./node_modules 下)
  >
  > 

* 一些坑

  * 启动vue项目时报错：code ELIFECYCLE
  
    > 执行`npm install`重新拉取即可。前提是已经安装好vue的脚手架。
  
  * Error: Cannot find module 'webpack/bin/config-yargs' 报错原因, webpack@4.X踩的坑~
  
    > 这个就是目前版本的webpack-dev-server@2.11.5 不支持 webpack@4.32.2
    >
    > npm i webpack-dev-server@3.3.2 -D
    >
    > 
    >
    > webpack4.0以上都要安装webpack-cli ,  否则报错如下:　　
    >
    > npm i  webpack-cli -D
    >
    > 
    >
    > npm i webpack webpack-cli webpack-dev-server -D
    >
  
  * webpack4 TypeError: compilation.mainTemplate.applyPluginsWaterfall is not a function
  
    > 这个是因为官方 html-webpack-plugin 没有及时更新支持 webpack4 导致的问题：
    >
    > "html-webpack-plugin": "^3.2.0",
  
  * 解决npm安装时出现run `npm audit fix` to fix them, or `npm audit` for details
  
    > npm audit fix 
    >
    > npm audit fix --force 
    >
    > npm audit