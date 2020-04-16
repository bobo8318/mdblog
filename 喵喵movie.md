* create vue project

  > // 通过vue cli 脚手架初始化项目
  >
  > vue create vue_project 
  >
  > //运行程序
  >
  > npm run serve
  >
  > 
  >
  > vue create is a Vue CLI 3 only command 使用如下命令升级安装vue cli3
  >
  > npm uninstall -g vue-cli
  > npm install -g @vue/cli

* vue.config.js配置

  ```
  module.exports = {
      /* 部署生产环境和开发环境下的URL：可对当前环境进行区分，baseUrl 从 Vue CLI 3.3 起已弃用，要使用publicPath */ 
      /* baseUrl: process.env.NODE_ENV === 'production' ? './' : '/' */
      publicPath: process.env.NODE_ENV === 'production' ? '/public/' : './',
      /* 输出文件目录：在npm run build时，生成文件的目录名称 */
      outputDir: 'dist',
      /* 放置生成的静态资源 (js、css、img、fonts) 的 (相对于 outputDir 的) 目录 */
      assetsDir: "assets",
      /* 是否在构建生产包时生成 sourceMap 文件，false将提高构建速度 */
      productionSourceMap: false,
      /* 默认情况下，生成的静态资源在它们的文件名中包含了 hash 以便更好的控制缓存，你可以通过将这个选项设为 false 来关闭文件名哈希。(false的时候就是让原来的文件名不改变) */
      filenameHashing: false,
      /* 代码保存时进行eslint检测 */
      lintOnSave: true,
      /* webpack-dev-server 相关配置 */
      devServer: {
          /* 自动打开浏览器 */
          open: true,
          /* 设置为0.0.0.0则所有的地址均能访问 */
          host: '0.0.0.0',
          port: 8066,
          https: false,
          hotOnly: false,
          /* 使用代理 */
          proxy: {
              '/api': {
                  /* 目标代理服务器地址 */
                  target: 'http://47.100.47.3/',
                  /* 允许跨域 */
                  changeOrigin: true,
              },
          },
      },
  }
  ```

* git 相关操作

  > git checkout -b createComponents 创建分支并切换到新分支
  >
  > git checkout createComponents 切换分支
  >
  > git branch 查看分支
  >
  > git log 查看操作记录
  >
  > git merge createComponents  --no-ff 合并分支
  >
  > git branch -d createComponents  删除分支
  >
  > //撤销回滚
  >
  > //git commit之前 未添加到暂存区的撤销(没有git add) 添加进暂存区的撤销(git add后)
  >
  > git checkout -- filename来撤销修改
  >
  > git checkout -- . 多个文件
  >
  > git reset HEAD 从暂存区撤销所有
  > git reset HEAD new_src/app/Http/Controllers/Frontend/KyHome/KyHomeApp.php
  >
  > //git commit之后
  >
  > git  revert 2842c8065322085c31fb7b8207b6296047c4ea3
  >
  > git reset --hard e377f60e28c8b84158 强制将缓存区和工作目录都同步到你指定的提交
  >
  > 
  >
  > git push -f origin master 强制提交
  >
  > 
  >
  > //忽略文件
  >
  > touch .gitignore ，生成“.gitignore”文件。
  >
  > bin/: 忽略当前路径下的bin文件夹，该文件夹下的所有内容都会被忽略，不忽略 bin 文件
  >
  > /bin: 忽略根目录下的bin文件
  >
  > /*.c: 忽略 cat.c，不忽略 build/cat.c
  >
  > debug/*.obj: 忽略 debug/io.obj，不忽略 debug/common/io.obj 和 tools/debug/io.obj
  >
  > **/foo: 忽略/foo, a/foo, a/b/foo等
  >
  > a/**/b: 忽略a/b, a/x/b, a/x/y/b等
  >
  > !/bin/run.sh: 不忽略 bin 目录下的 run.sh 文件
  >
  > *.log: 忽略所有 .log 文件
  >
  > config.php: 忽略当前路径的 config.php 文件
  >
  > 
  >
  > .gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。
  >
  > git rm -r --cached .
  > git add .
  > git commit -m 'update .gitignore'

* router-link

  * css

    > .router-link-active vue-router特有css

* 城市列表

  * ref ($refs)用法

    > ref 有三种用法：ref 被用来给DOM元素或子组件注册引用信息。引用信息会根据父组件的 $refs 对象进行注册。如果在普通的DOM元素上使用，引用信息就是元素; 如果用在子组件上，引用信息就是组件实例。只要想要在Vue中直接操作DOM元素，就必须用ref属性进行注册
    >
    > 
    >
    > var h2 = this.$refs.city_sort.getElementByTagName('h2')
    >
    > this.$refs.city_sort.parentNode.ScrollTop = h2[index].offsetTop

* 全局filter

  > Vue.filter("setWH", (url, arg)=>{
  >
  > ​	return url.replace(/w\.h/, arg)
  >
  > })
  >
  > img :src="item.url | setWH('128.80')"

* axios 多次请求

  ```
  const CancelToken = axios.CancelToken;
  let cancel;
  
  axios.get('/user/12345', {
    // 在options中直接创建一个cancelToken对象
    cancelToken: new CancelToken(function executor(c) {
      cancel = c;
    })
  });
  
  // 取消上面的请求
  cancel();
  
  
  <script>
  import axios from 'axios'
  import qs from 'qs'
  
  export default {
      methods: {
          request(keyword) {
              var that = this;
              var CancelToken = axios.CancelToken
              var source = CancelToken.source()
                
              // 取消上一次请求
              this.cancelRequest();
              
              axios.post(url, qs.stringify({kw:keyword}), {
                  headers: {
                      'Content-Type': 'application/x-www-form-urlencoded',
                      'Accept': 'application/json'
                  },
                  cancelToken: new axios.CancelToken(function executor(c) {
                      that.source = c;
                  })
              }).then((res) => {
                  // 在这里处理得到的数据
                  ...
              }).catch((err) => {
                  if (axios.isCancel(err)) {
                      console.log('Rquest canceled', err.message); //请求如果被取消，这里是返回取消的message
                  } else {
                      //handle error
                      console.log(err);
                  }
              })
          },
          cancelRequest(){
              if(typeof this.source ==='function'){
                  this.source('终止请求')
              }
          },
      }
  }
  </script>
  ```

* better_scroll

  * 安装
  
    > cnpm i -S better-scroll
  
  * nexttick: 需要在视图更新之后，基于新的视图进行操作。需要注意的是，在 created 和 mounted 阶段，如果需要操作渲染后的试图，也要使用 nextTick 方法
  
    ```
    this.$nextTick(() => {
            this.msg2 = this.$refs.msgDiv.innerHTML
    })
    ```
  
    