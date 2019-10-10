title:vue知识杂记（长期更新）
date: 2019-8-9
Category: 前端,vue
Tags: vue,前端
Authors: openui
Summary: vue知识杂记

### vue

* 原理
  * 数据双向邦定:通过Object.defineProperty()

    

* vue-router

  * 安装：npm install vue-router  --save-dev 

  * 使用： src 下新建 router 文件件 新建index.js

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
    		component:listdata
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
    <router-link to="/hello">go hello</router-link>
    
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
    	//唯一修改state的方法
    	mutation:{
    		increment(state){
    			state.x++;
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

  * 循环：

    ```
    v-for="(item, index) in list" :key="index"
    ```

  * 表单：

    ```
    
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


​      

* 事件总线 Eventbus
  * 