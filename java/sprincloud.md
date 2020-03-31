* 服务调用：restTemplate spring对http工具类（httpclient,okhttp）的封装

* 概述
  * 很多组件组成
    * eureka 注册中心
    * Gateway网关
    * Ribbon负载均衡
    * feign服务调用
    * Hystrix熔断器
  * 创建微服务工程
    * 父工程
    * 用户服务工程 service
    * 消费工程 consumer

* springcloud

  * dependency

    ```
     <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>2.0.5.RELEASE</version>
            <relativePath/> <!-- lookup parent from repository -->
       </parent>
        
       <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
            <java.version>1.8</java.version>
            <!--SpringCloud最新稳定版本-->
            <spring-cloud.version>Finchley.SR1</spring-cloud.version>
        </properties>
    
    <!--SpringCloud依赖版本管理-->
        <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>org.springframework.cloud</groupId>
                    <artifactId>spring-cloud-dependencies</artifactId>
                    <version>${spring-cloud.version}</version>
                    <type>pom</type>
                    <scope>import</scope>
                </dependency>
            </dependencies>
        </dependencyManagement>
    ```

    

* eureka ：

  spring cloud中discovery service有许多种实现（eureka、consul、zookeeper等等），@EnableDiscoveryClient基于spring-cloud-commons, @EnableEurekaClient基于spring-cloud-netflix。
   其实用更简单的话来说，就是如果选用的注册中心是eureka，那么就推荐@EnableEurekaClient，如果是其他的注册中心，那么推荐使用@EnableDiscoveryClient。

  * dependency

      * 服务端：@EnableEurekaServer注解
          ```
          //新版
          <dependency>
                      <groupId>org.springframework.cloud</groupId>
                     <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
         </dependency>
         
         //旧版
         <dependency>
                     <groupId>org.springframework.cloud</groupId>
                     <artifactId>spring-cloud-netflix-eureka-server</artifactId>
          </dependency>
         ```
         
      * provider：@EnableEurekaClient

        ```
        //新版
        <dependency>
                    <groupId>org.springframework.cloud</groupId>
                    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
      //旧版
         <dependency>
                    <groupId>org.springframework.cloud</groupId>
                    <artifactId>spring-cloud-starter-eureka</artifactId>
        </dependency>
        ```
        
      * consume:@EnableFeignClients

          * 依赖

          ```
           <dependency>
                 <groupId>org.springframework.cloud</groupId>
                 <artifactId>spring-cloud-starter-feign</artifactId>
             </dependency>
          
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                 <artifactId>spring-cloud-starter-eureka</artifactId>
           </dependency>
          ```

          * 使用

            ```
            //调用接口
            @FeignClient(value = "CART") // value 或者 name都可以
            public interface CartFeignClient {
            
                @PostMapping("/cart/{productId}")
                Long addCart(@PathVariable("productId")Long productId);
            }
            --------------------------------------------------------------------------
            //controller类中直接注入feign client
            @Autowired
            private CartFeignClient cartFeignClient;
            
            @PostMapping("/toCart/{productId}")
            public ResponseEntity addCart(@PathVariable("productId") Long productId){
                Long result = cartFeignClient.addCart(productId);
                return ResponseEntity.ok(result);
            }
            ```

            * 容错Hystrix feign中已经集成

              ```
              #yml 启用
              feign:
              	hystrix:
              		enabled: true
              ```

              

  * application.yml

    * 服务端

    ```
    # 服务名称
    spring:
      application:
        name: hengboy-spring-cloud-eureka
    # 服务端口号
    server:
      port: 10000
    
    #Eureka 相关配置
    
    eureka:
      server:
        enable-self-preservation: false           # 关闭自我保护模式（缺省为打开）
        eviction-interval-timer-in-ms: 5000       # 续期时间，即扫描失效服务的间隔时间（缺省为60*1000ms）
      client:
        service-url:
          defaultZone: http://localhost:${server.port}/eureka/
        # 是否从其他的服务中心同步服务列表
        fetch-registry: false
        # 是否把自己作为服务注册到其他服务注册中心
        register-with-eureka: false
    ```

    * 客户端

      ```
      # 服务名称
      spring:
        application:
          name: user-service
      eureka:
        client:
        	registry-fetch-interval-seconds: 5 # 默认为30秒
          service-url:
            defaultZone: http://localhost:10000/eureka/
          healthcheck:
            enabled: true      # 开启健康检查（依赖spring-boot-starter-actuator）
        instance:
        	ip-address: 127.0.0.1
        	prefer-ip-address: true
          lease-renewal-interval-in-seconds: 5 # 心跳时间，即服务续约间隔时间（缺省为30s）
          lease-expiration-duration-in-seconds: 10# 发呆时间，即服务续约到期时间（缺省为90s）
          
      ```

    * feign配置

      ```
      #feign的配置，连接超时及读取超时配置
      feign:
        client:
          config:
            default:
              connectTimeout: 5000
              readTimeout: 5000
              loggerLevel: basic
      ------------------------------------------------------------------------------
      # 开启gzip
      feign:
        compression:
          request: #请求
            enabled: true #开启
            mime-types: text/xml,application/xml,application/json #开启支持压缩的MIME TYPE
            min-request-size: 2048 #配置压缩数据大小的下限
          response: #响应
            enabled: true #开启响应GZIP压缩
      ```

      * 单独使用
      
        ```
        package pub.imba.config;
        
        import feign.Feign;
        import feign.Request;
        import feign.Retryer;
        import feign.auth.BasicAuthRequestInterceptor;
        import feign.jackson.JacksonDecoder;
        import feign.jackson.JacksonEncoder;
        import org.springframework.beans.factory.annotation.Qualifier;
        import org.springframework.context.annotation.Bean;
        import org.springframework.context.annotation.Configuration;
        import pub.imba.feignInterface.DataFeignInterface;
        
        @Configuration
        public class TestFeignConfig {
        	// 登录认证
            @Bean
            public BasicAuthRequestInterceptor basicAuthRequestInterceptor() {
                return new BasicAuthRequestInterceptor("dev1", "asfhunpjqw832h");
            }
        
            /**
             * FeignClient 配置
             * @return
             */
            @Bean
            DataFeignInterface dataFeignClient() {
                return Feign.builder()
                        //.client(new OkHttpClient())
                        //.logger(new TestApiFeignLogger())
                       // .logLevel(Logger.Level.FULL)
                        .requestInterceptor(basicAuthRequestInterceptor())
                        .encoder(new JacksonEncoder())
                        .decoder(new JacksonDecoder())
                        .options(new Request.Options(1000, 3500))
                        .retryer(new Retryer.Default(5000, 5000, 3))
                        .target(DataFeignInterface.class, "http://9eed78e3.ngrok.io");
            }
        }
        
        //
        package pub.imba.feignInterface;
        
        import com.luo.erlei.comm.out.Brief;
        import com.luo.erlei.comm.out.Ret;
        import feign.Param;
        import feign.RequestLine;
        import org.springframework.cloud.netflix.feign.FeignClient;
        import org.springframework.stereotype.Component;
        import org.springframework.web.bind.annotation.PathVariable;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RequestMethod;
        import org.springframework.web.bind.annotation.RequestParam;
        import pub.imba.impl.UserFeignClientFallBack;
        import pub.imba.model.MyUser;
        import pub.imba.util.ResultEntry;
        
        //@FeignClient(name="user-service")
        /@FeignClient(name="service",configuration = FeignClientConfiguration.class)
        
        //@Component
        public interface DataFeignInterface {
        
        
            //@RequestMapping(value = "/q/brief", method = RequestMethod.GET)
            //@RequestLine("GET /user/test?param={param}")
            //public ResultEntry test(@Param("param") String param);
        
            @RequestLine("GET /q/brief")
            public Ret<Brief> brief();
        
        
        }
        
        ```
      
        

* 高可用：要相互注册 本机的defaultZone 注册其他eureka的地址

  * yml

    ```
    server:
    	port: ${port:1086} 如果设置了port 用port 没用 用1086
    eureka:
      client:
        service-url:
          defaultZone: ${defaultZone:http://localhost:10000/eureka/}
    ```

    

![image-20191222185631422](C:\Users\My\AppData\Roaming\Typora\typora-user-images\image-20191222185631422.png)

* Ribbon负载均衡







* ### 一些常见问题

  * java.lang.IllegalStateException: RequestParam.value() was empty on parameter 0

    > @RequestParam(required = false) String XXCode
    >
    > 这个参数少了个value = "XXCode", 这个是Spring 4.0版本后，@RequestParam 注解对参数传值有了很好的封装特性并严格校验。
    >
    > 改为：@RequestParam(value = "XXCode", required = false) String XXCode

