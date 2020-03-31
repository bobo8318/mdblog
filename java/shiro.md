### 核心组件

* Subject:当前操作主体

* SecurityManager:安全管理器

* Realm:应用与数据安全的桥梁

### spring boot 引入shiro

* 依赖

    ```
    <dependency>
        <groupId>org.apache.shiro</groupId>
        <artifactId>shiro-spring</artifactId>
        <version>1.4.0</version>
    </dependency>
    ```

* 配置类

  ```
  @Configuration
  public class ShiroConfig{
	
  	@Bean
  	public ShiroFilterFactoryBean shiroFiler(@Qualifier("securityManager") SecurityManager securityManager){
  		ShiroFilterFactoryBean filter = new ShiroFilterFactoryBean()
  		filter.setSecurityManager(securityManager)
  		/**
  		* shiro 内置过滤器
  		*	anon:无需认证
  			authc:必须认证才能访问
  			user:使用remember me 可以访问
  			perms:　该资源必须得到资源权限才可以访问
  			role:该资源必须得到角色
  		**/
  		
  		Map<String, String> filterMap = new LinkedHashMap<String, String>();
  		
  		//filterMap.put("/*", "authc");
  		filterMap.put("/add", "authc");
  		filterMap.put("/update", "authc");
  		//filterMap.put("/login", "anon");
  		filter.setLoginUrl("/login")
  		filter.setFilterChainDefinitionMap(filterMap)
  		// 授权过滤器 拦截后默认会自动跳转到未授权页面401
  		filterMap.put("/add", "perms[user:add]");
  		// 设置未授权页面
  		filter.setUnauthorizedUrl("/unAuth")
  		return filter;
  	}
  	
  	@Bean(name="")
  	public SecurityManager securityManager(@Qualifier("userRealm") UserRealm realm){
  		DefatultWebSecurityManager manager = new DefatultWebSecurityManager();
  		manager.setRealm(realm)
  		return manager;
  	}
  	
  	@Bean(name="")
  	public UserRealm getUserRealm(){
  		return new UserRealm();
  	}
  }
  ```
  
  * UserRealm.class
  
    ```
    public class UserRealm extends AuthorizingRealm{
    	
    	@AutoWired
    	private UserService userService
    
    	//认证逻辑
    	@Overwrite
    	protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken arg0){
    		// 
    		
    		UsernamePasswordToken token = (UsernamePasswordToken)arg0;
    		
    		UserPo user = userService.getUser(token.getUsername())
    		
    		if(!token.getUsername().equals(name))(//　用户不存在
    			return null;//底层会抛出UnKnownAccountException
    		)
    		return new SimpleAuthenticationInfo("", token.getPassword(), "");
    	}
    	//授权逻辑
    	@Overwrite
    	protected AuthenticationInfo doGetAuthenticationInfo(PrincipalCollection pc){
    		String username = (String) pc.getPrimaryPrincipal();
    		User user = new User();
    		user.serUsername(username);
    		SimpleAuthenticationInfo info = new SimpleAuthenticationInfo();
    		info.addStringPermission("delete");
    		List roleList = userService.getRole(user);
    		if(roleList != null){
    			for(String role : roleList){
    				info.addRole(role);
    			}
    			return info;
    		}
    		return null;
    	}
    	
    }
    ```
  
    
  
  * LoginController
  
    ```
    @RequestMapping("/login")
    public String doLogin(String username, String password){
    	//　获取subject类
    	Subject subject = SecurityUtils.getSubject();
    	// 封装用户数据
    	UsernamePasswordToken token = new UsernamePasswordToken(username, password);
    	try{
    		// 执行登陆逻辑
    		subject.login(token);
    	}catch(){
    		
    	}
    
    }
    ```
  
  * controller添加
  
    > @RequiresPermissions("user:add")
    >
    > //编程方式
    >
    > Subject subject = SecurityUtils.getSubject();
    >
    > if(subject.hasRole("admin")){
    >
    > ​	//有权限
    >
    > }
  
  * thymeleaf & shiro
  
    * impoty thymeleaf
  
      ```
      com.github.theborakompanioni
      thtmeleaf-extras-shiro
      2.0.0
      ```
  
    * ShiroConfig 添加　ShiroDialect
  
      ```
      @Bean
      public ShiroDialect getShiroDialect(){
      	return new ShiroDialect();
      }
      ```
  
    * 使用
  
      ```
      <div　shiro:hasPermission="user:add">添加</div>
      <div　shiro:hasPermission name"add">添加</div>
      <div　shiro:hasAnyRoles name="user">添加</div>
      ```
  
      