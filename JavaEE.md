# Spring 核心容器

## 简介

本模块由 spring-core , spring-beans , spring-context , spring-context-support , and springexpression
(Spring Expression Language) 4 个模块组成。

## IoC和DI

**什么叫IoC**

IoC (Inversion of Control，控制反转) ，是面向对象编程中的一种设计原则，可以用来减低计算机代码之间的耦合度。只是因为该理论时间成熟相对较晚，并没有包含在GoF中。

系统中通过引入实现了IoC模式的IoC容器，即可由IoC容器来管理对象的生命周期、依赖关系等，从而使得应用程序的配置和依赖性规范与实际的应用程序代码分离。

从使用上看，以前手动new对象，并设置对象中属性的方式，控制权是掌握在应用程序自身。现在则全部转移到了容器，由容器来统一进行管理对象。因为控制权发生了扭转，所以叫控制反转。
**什么又是IoC容器**

实现了IoC思想的容器就是IoC容器，比如：SpringFremework, Guice（Google开源的轻量级DI框架）
**什么是DI**

DI (Dependency Injection，依赖注入) 是实现IoC的方法之一。所谓依赖注入，就是由IOC容器在运行期
间，动态地将某种依赖关系注入到对象之中。

所以，依赖注入（DI）和控制反转（IoC）是从不同的角度的描述的同一件事情，就是指通过引入 IoC 容
器，利用依赖关系注入的方式，实现对象之间的解耦。

## Spring使用流程

![1](https://gitee.com/wang-fuming/dawning/raw/master/1.jpg)





# Spring Boot

## 项目建立

通过start.spring.io建立

## 开发说明

SpringBoot 已经集成了 Tomcat，以后就不用像传统 Web 开发那样还需要下载一个 Tomcat 程序，配
置启动了。只需要启动生成的启动类即可。

## 默认的Web资源文件夹
SpringBoot 默认会使用 src/main/resources 目录下的如下文件夹作为Web资源文件夹：

1. /static：静态资源文件夹，如html，js，css等存放
2. /public：静态资源文件夹，同上
3. /templates：模版资源文件夹（后端模版框架使用的模版文件，会解析变量后再生成动态 html，
    我们不学，了解即可）
    注：在以上路径中的资源，服务路径不需要在前边再加 /static，/public。如在 static 文件夹下的
    home.html ，服务路径为：/home.html
    如果是使用普通Maven项目搭建，可以自行创建以上文件夹，在 src/main/resources 下创建
    public 和 static 文件夹即可。

##  默认的自动扫描

SpringBoot默认会扫描启动类所在包，只要位于该包以下的使用了Spring注解的类，都可以注册到容器
中，如以前学过的@Controller，@Service等。
示例：如启动类为 org.example.Application ，则可以扫描到
org.example.controller.LoginController 中的类注解@Controller。

## 默认的配置文件

SpringBoot默认使用 src/main/resource/application.properties 作为启动的配置文件，可以自
定义如启动端口等等配置。
如果是使用普通Maven项目搭建，在 src/main/resources 下创建 application.properties ，内容
为空即可。

## 默认的应用上下文路径

SpringBoot启动的Web项目，应用上下文路径默认为 /

## 启动类

如果是使用普通Maven项目搭建，可以自行编写启动类：类上使用 @SpringBootApplication 注解：

# Spring MVC

![Snipaste_2022-02-23_16-04-02](https://gitee.com/wang-fuming/dawning/raw/master/Snipaste_2022-02-23_16-04-02.png)

**Model（模型）**是应用程序中用于处理应用程序数据逻辑的部分。

通常模型对象负责在数据库中存取数据。
**View（视图）**是应用程序中处理数据显示的部分。

通常视图是依据模型数据创建的。
**Controller（控制器）**是应用程序中处理用户交互的部分。

通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

## @Controller

`@Controller`注解标注是一个类是Web控制器，其和`@Component`注解等价，只不过在Web层使用，其

便于区分类的作用。

## @RequestMapping

`@RequestMapping`是Spring Web应用程序中最常被用到的注解。

在对SpringMVC进行配置的时候，需要指定请求与处理方法之间的映射关系，这时候就需要使用

`@RequestMapping`注解。该注解可以在控制器类的级别和其方法级别上使用。

`@RequestMapping`注解能够处理的HTTP请求方法有：` GET, HEAD, POST, PUT, PATCH, DELETE,
OPTIONS, TRACE `。
为了能够将一个请求映射到一个特定的HTTP方法，你需要在@RequestMapping中使用method参数声
明HTTP请求所使用的方法类型。

```java
@RequestMapping("/test)
@RequestMapping(value="/index3",method = RequestMethod.GET)
```

## 控制器的方法返回

**String返回类型**
有两种使用方式：

1. 返回 URI 资源路径的字符串，可以使用 redirect:/服务路径 **表示重定向到某个路径**，
forward:/服务路径 **表示转发到某个路径**，如果前边不写**默认就是转发**。
2. `@RequestMapping`结合`@ResponseBody`，返回的字符串会作为响应体内容。此时响应的
Content-Type为 text/plain 普通文本。

没有注解返回的就是页面，有注解返回文本

```java
    //进行重定向
	@RequestMapping("/index1")
    public String getIndex1(){
        logger.error("这是跳转链接");
        System.out.println("这是跳转连接");
        return "redirect:/index.html";
    }
//进行转发
    @RequestMapping("/index2")
    public String getIndex2(){
        logger.error("这是请求转发");
        System.out.println("请求转发");
        return "forward:/index.html";
    }
//默认转发
    @GetMapping("/index4")
    public String getIndex4(){
        logger.error("我是 index4");
        return "/index.html";
    }
//返回字符串
    @ResponseBody
    @RequestMapping("/index6")
    public String getIndex6(){
        System.out.println("index6");
        return "index/html";
    }
```

**返回普通的Java类型**
返回类型为Object，一般使用带Getter，Setter方法的模型类

结合@ResponseBody使用，表示将对象序列化后的数据放在响应体返回

在SpringBoot中默认响应的Content-Type为 application/json

非字符串对象会自动序列化为 json 字符串

```java
	private final ObjectMapper mapper =new ObjectMapper();
    @RequestMapping("/index7")
    @ResponseBody
    public String getIndex7() throws JsonProcessingException {
        System.out.println("index7");
        User user=new User();
        user.setUsername("Java");
        user.setPassword("最好的语言");
        logger.error("index7函数");
        return mapper.writeValueAsString(user);
    }

    @RequestMapping("/index8")
    @ResponseBody
    public User getIndex8(){
        System.out.println("index8");
        User user=new User();
        user.setUsername("Java");
        user.setPassword("最好的语言");
        return user;
    }
```

**返回ResponseEntity**



## @ResponseBody

1. 返回类型为String，表示响应`Content-Type: text/plain`，且响应体为控制器方法的字符串返回值
2. 返回类型为普通Java类型，表示响应`Content-Type: application/json`，以返回对象序列化为json后
作为响应体。
3. `@ResponseBody`可以使用在类上，表示该类中所有方法都是默认以返回值作为响应体，也就是所
有方法都使用`@ResponseBody`。

## 控制器方法支持的参数类型

## @PathVariable

一般的 URI 服务路径都是固定的，SpringMVC提供了 restful 风格可以变化的 URI。

作用：使用URL的动态参数作为方法的参数

```java
    @RequestMapping("/people/{pid}/pets/{aid}")
    public String method1(@PathVariable("pid") String id1,@PathVariable("aid") String id2) {
        logger.error("用户id:"+id1+",宠物id:"+id2);
        return "用户id:"+id1+",宠物id:"+id2;
    }
```

1、{}是将服务路径 URI 中的部分定义为变量，之后在方法参数中获取该路径变量。更多格式可参考URI格式。
2、请求 /people/1/pets/2 ，显示的网页内容为： 主人id：1, 宠物id：2 。
3、变量已经定义了为String字符串，所以不能转换为字符串的 URI 都会报错。
4、变量名ownerId，petId必须和 URI 中的定义名称一致。

## @RequestParam

当请求数据要绑定到某个简单对象时，可以使用@RequestParam。

1、URL 中的请求数据queryString

2、请求头，Content-Type为表单默认提交的格式` application/x-www-form-urlencoded` ，请求体中的数据

3、请求头，Content-Type为 `multipart/form-data` ，请求体中的数据。form-data 可以提交文本数据，也可以提交二进制文件。

以上简单对象包括：基本数据类型、包装类型、MultipartFile（接收二进制文件）

## POJO对象

POJO（Plain Ordinary Java Object）：简单的 java 对象，实际就是属性提供了Getter，Setter方法的普通对象。

使用 java 对象和使用@RequestParam注解非常类似，只是有点细节不同：

@RequestParam是以方法参数变量名和传入的键对应，POJO对象作为方法参数时，是以POJO对象中的属性名对应传入的键

@RequestParam默认必须传入该请求数据，而 POJO 对象是根据请求数据来填充属性，如果请求
数据没有，则属性就是默认值（new对象时每个属性的默认值)。

```java
//和@RequestParam一样
@PostMapping("/pojo1")
public Object pojo1(String username, Integer count){
	Map<String, String> map = new HashMap<>();
	map.put("用户名", username);
	map.put("count", String.valueOf(count));
	return map;
}
//传入参数需要与字段对应
@PostMapping("/pojo2")
	public Object pojo2(User user){
	Map<String, String> map = new HashMap<>();
	map.put("用户名", user.getUsername());
	map.put("密码", user.getPassword());
	return map;
}
@PostMapping("/pojo3")
public Object pojo3(User user, MultipartFile file) throws IOException {
	Map<String, String> map = new HashMap<>();
	map.put("用户名", user.getUsername());
	map.put("密码", user.getPassword());
	map.put("文件名", file.getName()+", "+file.getOriginalFilename());
	map.put("文件类型", file.getContentType());
	map.put("文件大小", file.getSize()/1024+"KB");
	map.put("文件内容（二进制转字符串）", new String(file.getBytes()));
	return map;
}
```



## @RequestBody

4、当请求的数据类型Content-Type为` application/json `时，需要显示的使用`@RequestBody`注解

```java
    private static final String USERNAME="username";
    private static final String PASSWORD="password";
    @RequestMapping("/login")
    @ResponseBody
    public String login(@RequestBody User user, HttpServletRequest req){
        if(USERNAME.equals(user.getUsername())&&PASSWORD.equals(user.getPassword())){
            req.getSession().setAttribute("user",user);
            return "登录成功";
        }else{
            return "登录失败";
        }
    }
```

## @RequestPart

对于请求的数据类型Content-Type为 multipart/form-data 时，二进制文件除了以上@RequestParam和 POJO 对象的方式外，还可以使用@RequestPart

```java
    @RequestMapping("/register")
    public Object register(String username, @RequestPart MultipartFile file) throws IOException {
        //动态获取路径
        String path= Objects.requireNonNull(Objects.requireNonNull(ClassUtils.getDefaultClassLoader()).getResource("static")).getPath();
        System.out.println(username);
        logger.error(path);
        path+="/upload/";
        //获取文件名字，目的是获取文件格式
        String fileType=file.getOriginalFilename();
        assert fileType != null;
        fileType=fileType.substring(fileType.lastIndexOf("."));
        String fileName= UUID.randomUUID() +fileType;
        file.transferTo(new File(path+fileName));
        return null;
    }
```

## Servlet API

在控制器方法参数中，可以使用Servlet相关API，SpringMVC会自动将相关Servlet对象装配到方法参数
中，如 `HttpServletRequest `、`HttpServletResponse` 、`HttpSession` 等。

返回值设置为void，此时和在Servlet中开发差不多了。

当然也可以使用返回值，`SpringMVC`会自动跳转
页面（无`@ResponseBody`，返回类型为`String`），或返回`Content-Type: text/html`的网页内容（使用

`@ResponseBody`，返回类型为`String`），或返回 `json` 字符串（`@ResponseBody`，返回` POJO `对象）

## @RequestHeader

```java
@GetMapping("/header")
public String header(@RequestHeader("Accept-Encoding") String encoding,
@RequestHeader("User-Agent") String userAgent) {
return String.format("<p>Accept-Encoding: %s</p><p>User-Agent: %s</p>",
encoding, userAgent);
}
```

## CookieValue

```java
@GetMapping("/cookie")
public String cookie(@CookieValue("JSESSIONID") String cookie) {
	return String.format("JSESSIONID: %s", cookie);
}
```

## 自定义后端路径映射

SpringBoot中使用SpringMVC非常方便，SpringBoot提供了大部分的MVC默认功能，并且需要自定义

某部分功能也非常方便，在配置类中实现 WebMvcConfigurer 接口，根据需要重写方法即可：

```java
//注意事项1：这个注解将类注册，托管给框架
@Configuration
public class AppConfig implements WebMvcConfigurer {、
    @Override
    public void configurePathMatch(PathMatchConfigurer configurer) {
        configurer.addPathPrefix("api",c->true);
    }

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        System.out.println("拦截器启动");
        registry.addInterceptor(new LoginInterceptor()).addPathPatterns("/**");
    }
}
```

```java
@Override
public void configurePathMatch(PathMatchConfigurer configurer) {
	//Controller路径，统一添加请求的路径前缀，第二个参数，c是Controller类，返回boolean表示是否添加前缀
	//所有Controller请求路径，都要带/api的前缀
	configurer.addPathPrefix("api", c->true);
}
```

## 自定义拦截器

```java
//注意事项1：实现接口
@RestController
public class LoginInterceptor implements HandlerInterceptor {
    @Override
	public boolean preHandle(HttpServletRequest request, HttpServletResponseresponse, Object handler) throws Exception {
		HttpSession session = request.getSession(false);
		//session不为空，表示已登录
		if(session != null){
		//返回true，允许继续执行Controller中的方法
			return true;
		}
		//响应状态码设置为401
		response.setStatus(HttpStatus.UNAUTHORIZED.value());
		//返回false，不再执行Controller中的方法，直接响应一个空的响应体
		return false;
    }|
}

```

```java
@Override
public void addInterceptors(InterceptorRegistry registry) {
	registry.addInterceptor(new LoginInterceptor())
	.addPathPatterns("/api/**")//添加路径拦截规则，**表示下级多级目录的任意字符匹配
	.excludePathPatterns("/api/user/login");//排除登录路径
}
```

## @ControllorAdvice

**统一异常处理**

```java
//注意事项1：//在SpringBoot中使用，会扫描启动类所在包下所有@Controller类
@ControllerAdvice
public class ErrorException {
    //注意事项2：如果客户端请求，执行控制器方法抛Exception异常，会执行本方法
    @ExceptionHandler(Exception.class)
    //注意事项3：返回json字符串
    @ResponseBody
    public Object method1(Exception e){
        Map<String,Object> map=new HashMap<>();
        map.put("status",-1);
        map.put("data","");
        map.put("msg",e.getMessage());
        return map;
    }
}
```

**统一返回**

```java
//注意事项1：实现ResponseBodyAdvice接口，表示可以根据条件对返回的数据重写
public class MyResponseBody implements ResponseBodyAdvice {
    //注意事项2：Sring框架注入
    @Autowired
    private ObjectMapper objectMapper;

    //注意事项3：true表示开启，false表示关闭
    @Override
    public boolean supports(MethodParameter returnType, Class converterType) {
        return false;
    }

    @SneakyThrows
    @Override
    public Object beforeBodyWrite(Object body,
                                  MethodParameter returnType,
                                  MediaType selectedContentType,
                                  Class selectedConverterType,
                                  ServerHttpRequest request,
                                  ServerHttpResponse response) {
        HashMap<String,Object> map=new HashMap<>();
        map.put("status",0);
        map.put("data",body);
        map.put("msg","");
        //注意事项4：如果控制器方法返回类型为字符串，响应的Content-Type为text/plain，手动设置为json，并重写为序列化后的json字符串
        if(body instanceof String){
            response.getHeaders().setContentType(MediaType.APPLICATION_JSON);
            return objectMapper.writeValueAsString(map);
        }
        return map;
    }
}
create table user(
    id int primary key auto_increment,
    username varchar(50) not null,
    password varchar(32) not null,
    photo varchar(100) not null,
    createtime datetime default now(),
    updatetime datetime default now()
);
```



# MyBatis

## 使用

1、引入依赖

2、配置

在改路径下配置`application.properties`

```xml
# 数据库地址
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/mybatis_studycharactionEncoding=utf8&useSSL=true
# 数据库用户名
spring.datasource.username=root
# 数据库密码
spring.datasource.password=qwer1234
# 数据库驱动
spring.datasource.driver-class-name=com.mysql.jdbc.Driver

# 映射文件地址
mybatis.mapper-locations=classpath:/mapper/**Mapper.xml
```

3、声明映射接口

```java
//注意事项1：注解
@Mapper
@Component
//注意实现2：接口
public interface ArticleMapper {
	Article selectById(Integer id);
}
```

4、mapper.xml映射数据库

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="{关联的mapper接口全限定名}">
	<resultMap id="{结果集映射id}" type="{Java实体类}">
	<id column="{结果集唯一标识}" property="{实体类属性}" />
	<result column="{结果集字段1}" property="{实体类属性}" />
	<result column="{结果集字段2}" property="{实体类属性}" />
	</resultMap>
</mapper>
```

```java
	int add(User user);

    <insert id="add" parameterType="com.example.mybatis_study.model.User">
        insert into user(username,password,photo) values (#{username},#{password},#{photo})
    </insert>
```



## 查询

单一参数查询

```java
	User selectById(int id);
    <select id="selectById" 
        parameterType="java.lang.Integer" 
        resultType="com.example.mybatis_study.model.User">
       
        select * from user where id=#{id}
    </select>
```

多元素查询

```java
    //多个参数需要保证映射一致，不一致可以使用@Param实现一致
    User selectByNameAndPassword(@Param("name") String username, String password);
    <select id="selectByNameAndPassword" 
        parameterType="java.lang.String" 
        resultType="com.example.mybatis_study.model.User">
        
        select * from user where username=#{name} and password=#{password}

    </select>
        
    User selectByNameAndPassword(String username, String password);
    <select id="selectByNameAndPassword" 
        parameterType="java.lang.String" 
        resultType="com.example.mybatis_study.model.User">
        
        select * from user where username=#{username} and password=#{password}

    </select>

```

#和$的区别

对于 #{参数} 的使用来说，如果参数是字符串，在替换占位符时，会在 sql 语句中加上单引号。
如果是不能使用单引号的字符串，例如 sql 语句是 order by 字段 {传入参数} ，此时 {传入参数} 就需
要使用 ${传入参数} 这样的占位符，替换时不会带上单引号。

区别就是：#会给参数加上引号，而$不会

但也要注意由此带来sql注入问题

有关sql注入的问题

```java
username=username.replace("'", "").replace("or", "");//手动过滤信息
<select id="getListByName2" resultType="com.example.demo.model.User">
        select * from userinfo where username like concat('%',#{username},'%')
    </select>
    //使用mysql提供的方法进行拼接（t
```



获取自增主键

useGeneratedKeys：这会令 MyBatis 使用 JDBC 的 getGeneratedKeys 方法来取出由数据库内部生成的主键（比如：像 MySQL 和 SQL Server 这样的关系型数据库管理系统的自动递增字段），默认值：false。

keyColumn：设置生成键值在表中的列名，在某些数据库（像 PostgreSQL）中，当主键列不是表中的第一列的时候，是必须设置的。如果生成列不止一个，可以用逗号分隔多个属性名称。

keyProperty：指定能够唯一识别对象的属性，MyBatis 会使用 getGeneratedKeys 的返回值或insert 语句的 selectKey 子元素设置它的值，默认值：未设置（ unset ）。如果生成列不止一个，可以用逗号分隔多个属性名称。

```java
    <insert id="add" parameterType="com.example.mybatis_study.model.User"
    useGeneratedKeys="true" keyProperty="id" keyColumn="id">
        insert into user(username,password,photo) values (#{username},#{password},#{photo})
    </insert>
```



1、先创建一个实体对象

2、在mappper接口定义查询方法

3、在mapper.xml定义resultMap映射和association

## 动态sql

