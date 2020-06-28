# mybatis plus

Address: https://mp.baomidou.com/guide/quick-start.html

* Quick start

  ```
  //create table
  DROP TABLE IF EXISTS user;
  
  CREATE TABLE user
  (
  	id BIGINT(20) NOT NULL COMMENT '主键ID',
  	name VARCHAR(30) NULL DEFAULT NULL COMMENT '姓名',
  	age INT(11) NULL DEFAULT NULL COMMENT '年龄',
  	email VARCHAR(50) NULL DEFAULT NULL COMMENT '邮箱',
  	PRIMARY KEY (id)
  );
  DELETE FROM user;
  
  INSERT INTO user (id, name, age, email) VALUES
  (1, 'Jone', 18, 'test1@baomidou.com'),
  (2, 'Jack', 20, 'test2@baomidou.com'),
  (3, 'Tom', 28, 'test3@baomidou.com'),
  (4, 'Sandy', 21, 'test4@baomidou.com'),
  (5, 'Billie', 24, 'test5@baomidou.com');
  -- true develop : version （  乐观锁）deleted gmt_create fmt_modified
  
  //dependency
  	//maven
  	<parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.3.1.RELEASE</version>
      <relativePath/>
  </parent>
  <dependencies>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-test</artifactId>
          <scope>test</scope>
      </dependency>
      <dependency>
          <groupId>org.projectlombok</groupId>
          <artifactId>lombok</artifactId>
          <optional>true</optional>
      </dependency>
      <dependency>
          <groupId>com.baomidou</groupId>
          <artifactId>mybatis-plus-boot-starter</artifactId>
          <version>3.3.2</version>
      </dependency>
      <dependency>
          <groupId>com.h2database</groupId>
          <artifactId>h2</artifactId>
          <scope>runtime</scope>
      </dependency>
  </dependencies>
  
  //application.yml
  # DataSource Config
  spring:
    datasource:
      driver-class-name: org.h2.Driver
      schema: classpath:db/schema-h2.sql
      data: classpath:db/data-h2.sql
      url: jdbc:h2:mem:test
      username: root
      password: test
  ```

* mybatis plus 

  * pojo

    ```
    @Data
    @AllArgsConstructor
    @NoArgsConstructor
    
    @TableName(value = "dc_measure")//指定表名
    public class Dc_measure {
    
        @TableId(value = "id",type = IdType.AUTO)//指定自增策略
        private int id;
    
        private String measure_name;
    
    
    }
    ```

  * mapper

    ```
    @Mapper
    public interface DcMeasureMapper extends BaseMapper<Dc_measure> {
    }
    ```

  * test

    ```
     System.out.println(("----- selectAll method test ------"));
     List<Dc_measure> userList = measureMapper.selectList(null);
     Assert.assertEquals(3, userList.size());
     userList.forEach(System.out::println);
    ```

* config log

  ```
  //yml
  mybatis-plus:
    configuration:
      log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  ```

* CRUD

  * 数据库插入默认id（雪花算法）

    > @TableId(value = "id",type = IdType.AUTO)//指定自增策略

* 自动填充

  * all tables : gmt_created, gmt_modified

    > 1.database
    >
    > 'createTime' timestamp DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    >
    > 'moditiyTime' timestamp DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP  COMMENT '更新时间',
    >
    > 
    >
    > 2.code
    >
    > @TableField(fill = FieldFill.INSERT)
    > private Date createtime
    > @TableField(fill = FieldFill.INSERT_UPDATE)
    > private Date updatetime

    

    3.处理器

    ```
    @Component // mybatis 自动使用
    @Slf4j
    public class MyHandler implements MetaObjectHandler {
    
        @Override
        public void insertFill(MetaObject metaObject) {
            log.info("start insert fill");
            this.setFieldValByName("createTime", new Date(), metaObject);
            this.setFieldValByName("updateTime", new Date(), metaObject);
        }
    
        @Override
        public void updateFill(MetaObject metaObject) {
            this.setFieldValByName("updateTime", new Date(), metaObject);
        }
    }
    ```

* 乐观锁&悲观锁

  * 乐观锁实现方式：

    - 取出记录时，获取当前version
    - 更新时，带上这个version
    - 执行更新时， set version = newVersion where version = oldVersion
    - 如果version不对，就更新失败

  * 实体类加注解

    > @Version //乐观锁
    >   private Integer version;

  * 注册组件

    ```java
    @Bean
    public OptimisticLockerInterceptor optimisticLockerInterceptor() {
        return new OptimisticLockerInterceptor();
    }
    ```

* 查询操作

  ```
   Map<String, Object> params = new HashMap<String, Object>();
   List<Dc_measure> userList = measureMapper.selectByMap(null);
  ```

* 分页

  * 配置拦截器

    ```java
    @Bean
    public PaginationInterceptor paginationInterceptor() {
      PaginationInterceptor paginationInterceptor = new PaginationInterceptor();
      // 设置请求的页面大于最大页后操作， true调回到首页，false 继续请求  默认false
      // paginationInterceptor.setOverflow(false);
      // 设置最大单页限制数量，默认 500 条，-1 不受限制
      // paginationInterceptor.setLimit(500);
      // 开启 count 的 join 优化,只针对部分 left join
      paginationInterceptor.setCountSqlParser(new JsqlParserCountOptimize(true));
      return paginationInterceptor;
    }
    ```

  * 使用

    > Page<User> page = new Page<>(1,5);// 1当前页 5页面大小
    >
    > userMapper.selectPageVo(page, state);

* 删除

  * 普通删除

  * 逻辑删除

    ```
    //yml
    mybatis-plus:
      global-config:
        db-config:
          logic-delete-field: flag  #全局逻辑删除字段值 3.3.0开始支持，详情看下面。
          logic-delete-value: 1 # 逻辑已删除值(默认为 1)
          logic-not-delete-value: 0 # 逻辑未删除值(默认为 0)
    
    
    @TableLogic
    private Integer deleted;
    
    
    @Bean//3.3.0不需要bean
    public ISqlInjector sqlInjector(){
    	return new LogicSqlInjector();
    }
    
    ```

    

* 性能分析插件：慢查询

  * 1.导入插件

    ```java
    @Bean//3.2.0以上版本已移除 使用https://mp.baomidou.com/guide/p6spy.html
        @Profile({"dev","test"})// 设置 dev test 环境开启
        public PerformanceInterceptor performanceInterceptor() {
            PerformanceInterceptor tt = new PerformanceInterceptor();
            tt.setMaxTime(1);
            tt.setFormat(true);
            return tt;
        }
    ```

  * 2.测试使用

* 条件构造器：wrapper https://mp.baomidou.com/guide/wrapper.html#abstractwrapper

  ```
  QueryWrapper<User> wrapper = new QueryWrapper<>();
  wrapper.eq("name", "zhangsan");
  wrapper.notLike("name", "zhangsan").likeRight("name", "li");
  
  //子查询
  wrapper.inSql("id", "select id from user where id<3");
  
  //排序
  wrapper.orderByDesc("id")
  
  
  ```

  