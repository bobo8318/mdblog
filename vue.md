title:vue知识杂记（长期更新）
date: 2019-8-9
Category: 前端,vue
Tags: vue,前端
Authors: openui
Summary: vue知识杂记

### vue

* ide ：vscode 插件 vutr

* 非脚手架使用

  * 引用

    >  cdn 上下载vue.js https://www.bootcdn.cn/
    >  创建index.html 引入vue.js
    >  引入main.js
    
  * 使用

    ```
    //main.js
        let app = new Vue({
        	components:{
              piechart
             },
            el:"#app",
            data:{
               title:"hello" 
            },
            methods:{
            	method0(msg){
            		console.info(msg);
            	},
            	method1: function(){
            	
            	}
            },
            mounted() {
            	this.methon0(this.title)
            }
        });
    ```

  * 自定义组件

    ```
    全局组件：-----------------------------------------------------------
    let like = Vue.extend({
        template: `
            <div>
                <h2>全局组件定义方法一</h2>
                <p>全局组件定义方法一内容</p>
            </div>
        `
    });
    Vue.component('like-com', like);
    
    局部组件：----------------------------------------------------------
    let like = Vue.extend({
        template: `
            <div>
                <h2>局部组件定义方法一</h2>
                <p>局部组件定义方法一内容</p>
            </div>
        `
    });
    new Vue({
        el: '#app1',
        components: {
            'like-com': like 或者 直接写 like
        }
    });
    
    使用template定义---------------------------------------------------------
    <div id="app1">
        <my-love></my-love>
    </div>
    
    <template id="temp-com">
        <div>
            <h3>使用template定义的组件</h3>
            <p>使用template定义的组件的内容！</p>
        </div>
    </template>
    
    Vue.component('my-love', {
        template: '#temp-com'
    });
    
    使用script定义---------------------------------------------------------------
    
    <div id="app1">
        <my-love></my-love>
    </div>
    
    <script type="text/template" id="temp-com">
        <div>
            <h3>使用template定义的组件</h3>
            <p>使用template定义的组件的内容！</p>
        </div>
    </script>
    ```

  * 父子组件通信:

    ```
    父向子传递数据 通过props----------------------------------------------------------
    <div id="app">
        <my-comp :username="nickname"></my-comp>
    </div>
    
    Vue.component('my-comp', {
        props: ['username'],
        template: '<h3>{{ username }}</h3>'
    });
    
    new Vue({
        el: '#app',
        data: {
            nickname: '小七'
        }
    })
    ```

  * 使用

    >  <component :is="currentTab"></component>
    
  * 过滤器
    
    ```
    filters:{
            watchFilter: function(value){
                if(value == 1){
                    return "已收藏";
                }else{
                    return "收藏";
                }
            },
            isActiveFitlter: (value)=>{
                return value===1?'激活':'冻结'
            }
        },
        
    / 双花括号中
    {{ isActive | isActiveFitlter}}
    
    // 在v-bind 中
    <div v-bind:id=" isActive | isActiveFitlter"></div>
    ```
    
    * 全局 Filter
    
      ```
      /filters.js
      let isActiveFitlter = value => {
          return value===1?'激活':'冻结'
      }
      export { isActiveFitlter }
      
      
      //main.js 引入 filters.js
      import * as filters from './assets/common/filters'
      Object.keys(filters).forEach(key => {
          Vue.filter(key, filters[key])
      })
      ```
    
    * 注意在table中使用需要借助 ****\*插槽\*****
    
      ```
      <el-table-column prop="isActive" label="状态">
           <template slot-scope="scope">
                {{scope.row.isActive | isActiveFitlter}}
           </template>
      </el-table-column>
      ```
    
      
    
  * 列表排序

  

    

* 原理
  
* 数据双向邦定:通过Object.defineProperty()
  
* vue-router

  * 安装：npm install vue-router  --save-dev 

  * 使用： src 下新建 router 文件件 新建index.js

  * @ 相当于 src目录

    ```
    import Vue from 'vue'
    import Router from 'vue-router'
    import HelloWorld from '@/component/helloworld.vue'
    Vue.use(Router)
    
    export default new Router({
    	route:[
    		{
    			path:'/',
    			name:'helloworld',
    			component:Helloworld,
    			redirect:'/index',
    			alias:'hello'
    		},
    		{
    		//动态路由带参数 ：开头
    		path:'/list/:id',
    		//可以不通过this.$router获取：id
    		//直接当组件的props使用
    		props:true,
    		//通过name跳转
    		name:'listdata',
    		component: () => import('@/component/listdata.vue')
    		}
    	
    	]
    })
    
    export default{
    	name:'hello',
    	props:['id'],
    	mounted(){
    		console.log(this.id);
    	}
    }
    ```

    

  * 引用： main.js import router from './router'

  * 导航使用：

    ```
    <keep-alive><router-view></keep-alive>//缓存页面
    
    <router-link tag="li" to="/hello">go hello</router-link>
    
    <router-link :to="{name:'view1'}">go hello</router-link>
    
    <div @click="goto">function jump</div>
    
    methods:{
    	goto(){
    		this.$router.push('/hello2')
    	}
    }，
    mounted(){
    	//获取路由参数
    	console.log(this.$router.param.id)
    }
    
    //vue 自带的css选中样式
    li.router-link-active:{}
    // 错误路由地址重定向
    {
    	path:"/*"
    	redirect: "index"
    }
    ```

  * 路由导航守卫

    ```
    // 导航守卫
    // 使用 router.beforeEach 注册一个全局前置守卫，判断用户是否登陆
    router.beforeEach((to, from, next) => {
      if (to.path === '/login') {
        next();
      } else {
        let token = localStorage.getItem('Authorization');
     
        if (token === 'null' || token === '') {
          next('/login');
        } else {
          next();
        }
      }
    });
    ```

    

* vuex

  * 安装：npm install vuex -s

  * 使用：新建文件夹 store 新建index.js

    ```
    import Vue from 'vue';
    import Vuex from 'vuex';
    Vue.use(Vuex);
    export default new Vuex.Store({
    	plugin:[createLogger()],
    	state:{
    		x:1
    	},
    	getters:{//类似 compute 属性  this.$store.getters.showName
    		showName: state =>{
    			return state.logininfo.showName;
    		}
    	}
    	//唯一修改state的方法
    	mutation:{
    		increment(state){
    			state.x++;
    		}
    	},
    	actions:{ //注册actions 类似 vue里的method this.$store.dispatch("loginfun", param);
    		loginfun(context, param){
    			context.commit("login", param);//调用mutation中定义的方法
    		}
    	
    	}
    })
    
    Index.vue
    import store from 'Vuex'
    
    export default{
        	methods:{
        		add(){
        			this.$store.commit('increment');
        		},
        		getx(){
        			return this.$store.state.x
        		}	
        	}
        }
    
    
    // mapMutations
    
    import { mapMutations } from 'vuex'
    
     methods:{
         ...mapMutations( [ 'add','reduce' ] )
     }
     
     // 直接调用即可
     <button @click='add'>加</button>
    <button @click='reduce'>减</button>
    ```
  
* vue

  * 条件渲染

    ```
    <div v-if="type === 'A'">
          A
        </div>
        <div v-else-if="type === 'B'">
          B
        </div>
        <div v-else-if="type === 'C'">
        C
        </div>
      <div v-else>
          Not A/B/C
      </div>
      
        <template v-if="ok">
          <h1>Title</h1>
          <p>Paragraph 1</p>
          <p>Paragraph 2</p>
        </template>
        // v-sow
      <h1 v-show="ok">Hello!</h1>
    ```
    
    
    
  * 循环：
  
    ```
  v-for="(item, index) in list" :key="index"
  
    <li v-for="(value, key, index) in object" @click="getDataId(index)">
         {{ index }}. {{ key }} : {{ value }}
    </li>
    ```
  
  * VUE列表的搜索和排序：
  
    ```
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <div id="demo">
            <input type="text" v-model="searchName">
            <ul>
                <li v-for="(p,index) in filterPersons":key="index">
                    {{index}}---{{p.name}}---{{p.age}}
                </li>
            </ul>
            <button @click="setOrderType(1)">年龄升序</button>
            <button @click="setOrderType(2)">年龄降序</button>
            <button @click="setOrderType(0)">原本顺序</button>
        </div>
    </body>
    <script src="../js/vue.js"></script>
    <script>
        new Vue({
            el:'#demo',
            data:{
                searchName:'',
                orderType:0,//0代表原本顺序，1代表升序，2代表降序
                persons:[
                    {name:'Tom',age: 18},
                    {name:'coc',age: 16},
                    {name:'jjj',age: 17},
                    {name:'xxx',age: 19},
                ]
            },
          computed:{
  
                filterPersons(){
                    //取出相关的数据
                    const {searchName,persons,orderType} = this
                    //最终需要显示的数组
                    let fPersons;
                    //对persons进行过滤
                    fPersons=persons.filter(p => p.name.indexOf(searchName)!== -1)
                    //排序
                    if (orderType!==0){
                        fPersons.sort(function (p1,p2) { //如果返回负数，p1在前，返回正数，p2在前
                            //1代表升序，2代表降序
                            if (orderType===2){
                                return p2.age-p1.age;
                            } else {
                                return p1.age-p2.age;
                            }
        
                        })
                    }
                    return fPersons;
                }
            },
            methods:{
                setOrderType(orderType){
                    this.orderType = orderType;
                }
            }
        })
    </script>
    </html>
    ```
  
  * event bus 事件总线
  
    - 父组件会通过`props`向下传数据给子组件，当子组件有事情要告诉父组件时会通过`$emit`事件告诉父组件。
  
      ![https://www.w3cplus.com/sites/default/files/blogs/2018/1809/1488038869_67673.png]()
  
    ```
    //eventbus.js
        import Vue from 'vue' 
    export const EventBus = new Vue()
      
        // main.js Vue.prototype.$EventBus = new Vue()
       
    
    
        Bus.$emit('getTarget', event.target);   
        
        Bus.$on('getTarget', target => {  
                    console.log(target);  
                });  
    ```
  
  * css 控制
  
    ```
    <div :style = "margin: length+'px' "></div>   
        data(){
            return {
                length: 1,
            }
        }
        -------------------------------------------------------------------------------
        <div :class="{'youClass': isShow}"></div>
        data(){
          return {
                isShow: true ,
            }
        }
        -------------------------------------------------------------------------------
        :style="(currentGames.list[2].id==3)?'display:none':'display:flex'"
    ```
  
* slot 插槽

  * 将父组件放在子组件标签里的内容，放到想让他显示的地方,如下 如果子组件中没有slot 父组件的hello就不会显示出来。加入slot 父组件的包含内容 插到slot里

  ```
    //子组件
    <template>
      <div>
            <h3>我是子组件</h3>
            <slot></slot>//加了个slot标签，在父组件中，就可以让子组件标签内的内容显示啦
        </div>
    </template>
     //父组件
      <template>
       <div>
          //hello显示
           <v-child>hello</v-child>
        </div>
      </template>
  ```

​    ​   

  * 具名slot 子组件在对应分发的位置的slot标签里, 没有具名的内容会放到一个 子组件的默认插槽中 如果没有默认插槽就不显示。

    ```
    //子组件
    <template>
        <div>
            <h3>我是子组件</h3>
            <p><slot name="header">父组件中没header的时候会显示</slot></p>
            <p><slot name="footer">父组件中没footer的时候会显示</slot></p>
        </div>
    </template>
    
    //父组件
    <template>
      <div>
          <v-child>
              <p>hello</p>
              <h3 slot="header">header</h3>
          </v-child>
      </div>
    </template>
    
    ```

  * slot-scope:作用域插槽，可以接收子组件传来的数据

    ```
    // 父组件中
    <slot-scope-child>
        <template slot-scope="user">
           <ul>
            	<li v-for="(item, index) in user.data" :key="index">{{item}}</li>
           </ul>
        </template>
    </slot-scope-child>
    // 子组件中
    <div class="child">
        <h3>这里是子组件</h3>
        <slot :data="data"></slot>
    </div>
    
    数据在子组件，然后绑到父组件，父组件就可以使用了
    
    ```
    
  * 父子组件间通信

    * 父到子

      * 子组件中 props:['msgFather'] 接收父组件
      * 父组件中 msg-father="dad无可奉告" 绑定数据

    * 子到父

      * ```
        //子组件
        this.$emit("sendiptVal", this.inputValue) 
        //子组件发射自定义事件sendiptVal 并携带要传递给父组件的值，
        // 如果要传递给父组件很多值，这些值要作为参数依次列出 如 this.$emit('valueUp', this.inputValue, this.mesFather); 
        
        //父组件
        <accept-and-refuse @sendiptVal='showChildMsg'></accept-and-refuse>
        
        ```

    * 兄弟间

* 网络请求

  * axios

    *  安装注册使用：npm i axios

    * 拦截器

  ```
      axios.interceptors.request.use(
      	config => {
      		if (localStorage.getItem('loginToken')) {
                config.headers.Authorization = localStorage.getItem('loginToken');
              }
      		
      		return config;
      	},
      	error => {
          return Promise.reject(error);
        }
      )
      
  ```


* 事件总线 Eventbus
  
* 
  
* 一些问题

  * watch无法监听变化

    ```
    watch: {
        option: {
            handler(newVal) {
                console.log(newVal);
            },
            deep: true,
            immediate: true
        }
    },
    ```

  * $emit传入的事件名称**只能使用小写，不能使用大写**的驼峰规则命名

* 数组变化操作

    > push()//末尾添加
    >
    > pop()//末尾删除
    >
    > shift()//开头删除
    >
    > unshift()//开头添加
    >
    > splice()//添加splice(start,0, newitem) 删除splice(start, length) 替换splice(start, length, newitem)
    >
    > sort()//排序
    >
    > reverse()
    >
    > 控制台中操作数组
    >
    > exmples.items.push({message:"hello"})
    >
    > 可以触发界面更新数组操作
    >
    > example.items.$set(0, {message:'change'})
    >
    > $remove(item)

* 过滤器       //返回新数组 原数组不变

  > var arr_filter = arr.filter(function(element,  index, self){
  >
  > ​	return self.indexOf(element) == index;
  >
  > });

* 拼接 concat

  > arr.concat(["A","B","C"]);

* every & some 返回boolean 值

  > every 找到不符合的停止
  >
  > some  找到符合的停止
  >
  > arr.some(function(item, index, array){
  >

* vue-cli关闭/禁用/使用ESLint语法检测功能

    >  在项目的本目录下面config—index.js 文件夹中配置一下就可以禁用useEslint设为false