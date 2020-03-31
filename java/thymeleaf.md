* 依赖

  ```
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-thymeleaf</artifactId>
  </dependency>
  
  <dependency>
    <groupId>net.sourceforge.nekohtml</groupId>
    <artifactId>nekohtml</artifactId>
    <version>1.9.15</version>
  </dependency>
  ```

  

* html 模板引入

  > <html xmlns:th="http://www.thymeleaf.org">

* yml 配置

  ```
  spring:
    thymeleaf:
      mode: LEGACYHTML5
      cache: false
  ```

  