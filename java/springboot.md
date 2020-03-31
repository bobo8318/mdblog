title:springboot 知识汇总
date: 2019-9-22
Category: java
Tags: springboot,mybatis
Authors: openui
Summary: springboot 知识记录

### springboot

* mybatis

  * mybatis plus mybatis增强工具

    ```
    // 实体类
    @Data
    @TableName(value = "user")
    public class User{
    	@TableField(value = "age")
    	private Integer userAge;
    }
    
    // mapper
    @mapper
    public interface Usermapper extends BaseMapper<User>{
    	
    }
    
    // 分页
    @Bean
    public PaginationInterceptor paginationInterceptor(){
    	return new PaginationInterceptor();
    }
    ```

  * 注解方式获得自增id
  
    ```
    @Insert("insert into tbl_user (name, age) values (#{name}, #{age})")
    @Options(useGeneratedKeys=true, keyProperty="userId", keyColumn="id")
    void insertUser(User user);
    ```
  
    
  
  * pagehelper :分页工具


      > compile('com.github.pagehelper:pagehelper-spring-boot-starter:1.2.3')
    
    * properties
    
      ```
      pagehelper.helperDialect=mysql
      pagehelper.reasonable=true
      pagehelper.supportMethodsArguments=true
      pagehelper.params=count=countSql
      pagehelper.page-size-zero=true
      ```
    
    * 参数说明
    
      ```
      //当前页
      private int pageNum;
      //每页的数量
      private int pageSize;
      //当前页的数量
      private int size;
      //当前页面第一个元素在数据库中的行号
      private int startRow;
      //当前页面最后一个元素在数据库中的行号
      private int endRow;
      //总记录数
      private long total;
      //总页数
      private int pages;
      //结果集
      private List<T> list;
      //第一页
      private int firstPage;
      //前一页
      private int prePage;
      //是否为第一页
      private boolean isFirstPage;
      //是否为最后一页
      private boolean isLastPage;
      //是否有前一页
      private boolean hasPreviousPage;
      //是否有下一页
      private boolean hasNextPage;
      //导航页码数
      private int navigatePages;
      //所有导航页号
      private int[] navigatepageNums;
      ```
    
      * 使用
    
        ```
        PageHelper.startPage(page, size);
        List<UserInfo> userInfoList = userInfoMapper.selectAll();
        PageInfo<UserInfo> pageInfo = new PageInfo<>(userInfoList);
        ```


​        

* test:spring-boot-starter-test

  ```
  @RunWith(SpringRunner.class)
  @SpringBootTest
  ```

  * mockmvc

    ```
     @AutoConfigureMockMvc
     
     @MockBean //  @MockBean 会将mock的bean替换掉 SpringBoot 管理的原生bean，从而达到mock的效果。
      private XXXDao xxxtDao;
      
      
      Mockito.when(
            xxxDao.findMapBySql(
                    Mockito.anyString(),Mockito.anyList()
            )
     ).thenReturn(dataList);
     
     
     // http请求
     
    //配置MockMvc
    @Autowired
    protected MockMvc mockMvc;
    @Test
    public void TestXXX() throws Exception {
           MvcResult result = mockMvc.perform(
                    MockMvcRequestBuilders.get("/xxxController/xxx_query")
                            .contentType(MediaType.APPLICATION_JSON_UTF8)      
                            .param("xxx","xxx")
                        
    
            		)
                    .andExpect(MockMvcResultMatchers.status().isOk())
                    .andDo(MockMvcResultHandlers.print())
                    .andReturn();
           
        }
    ｝
    //静态导入 简化
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

    String content = "{\"username\":\"pj_mike\",\"password\":\"123456\"}";
    mockMvc.perform(request(HttpMethod.POST, "/user")
            .contentType("application/json").content(content))
            .andExpect(status().isOk())
            .andExpect(content().string("ok"));

    
    ```
    
    
    
    | .perform()   | 执行一个MockMvcRequestBuilders请求。其中`.get()`表示发送get请求（可以使用get、post、put、delete等）；`.contentType()`设置编码格式；`.param()`请求参数,可以带多个。 |
    | ------------ | ------------------------------------------------------------ |
    | andExpect()  | 加 MockMvcResultMatchers验证规则，验证执行结果是否正确       |
    | .andDo()     | 添加 MockMvcResultHandlers结果处理器,这是可以用于打印结果输出。 |
    | .andReturn() | 结果还回，然后可以进行下一步的处理。                         |
    
    
    
  * 单元测试的时候，如果不想造成垃圾数据，可以开启事务功能，在方法或类头部添加 @Transactional 注解即可
  
  * 真实Web环境进行测试
  
    ```
    @RunWith(SpringRunner.class)
    @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
    public class UserControllerTest3 {
      @Autowired
      private TestRestTemplate testRestTemplate;//RestTemplate的一种替代品
      @Test
      public void userMapping() throws Exception {
        User user = new User();
        user.setUsername("pj_pj");
        user.setPassword("123456");
        ResponseEntity<String> responseEntity = testRestTemplate.postForEntity("/user", user, String.class);
        System.out.println("Result: "+responseEntity.getBody());
        System.out.println("状态码: "+responseEntity.getStatusCodeValue());
      }
    }
     
     
     MultiValueMap,StringUtils,HttpEntity,ResponseEntity
    ```
  
    





* configuration

  ```
  
  @Bean("primaryDataSource")
  @Primary
  @ConfigurationProperties("primary.datasource")
  public DataSource buildPrimaryDataSource() {
  	return DataSourceBuilder.create().build();
  
  }
  
  
  @Component
  @ConfigurationProperties("sharding.datasource")
  public class DataSourceConfig {
  	private String url;
  	
  	public String getUrl() {
  		return url;
  	}
   
  	public void setUrl(String url) {
  		this.url = url;
  	}
  
  }
  ```

  