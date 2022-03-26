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

## if标签

```xml
<insert id="insert" parameterType="org.example.model.User"
useGeneratedKeys="true" keyProperty="id">
    insert into user(
	username,
	password,
	nickname,
	<if test="sex != null">
		sex,
	</if>
	birthday,
	head
	) values (
	#{username},
	#{password},
	#{nickname},
	<if test="sex != null">
		#{sex},
	</if>
	#{birthday},
	#{head}
    )
</insert>
```

##  trim标签

之前的插入用户功能，只是有一个 sex 字段可能是选填项，如果有多个字段，一般考虑使用<trim>标签
结合<if>标签，对多个字段都采取动态生成的方式。
<trim>标签中有如下属性：
	prefix：表示整个语句块，以prefix的值作为前缀
	suffix：表示整个语句块，以suffix的值作为后缀
	prefixOverrides：表示整个语句块要去除掉的前缀
	suffixOverrides：表示整个语句块要去除掉的后缀

```xml
    <insert id="addArticle">
        insert into article(title,content,uid
        <trim prefix="," suffixOverrides=",">
            <if test="count!=0">count,</if>
            <if test="state!=0">state,</if>
        </trim>)values(
                #{title},#{content},#{uid}
                <trim prefix="," suffixOverrides=",">
                    <if test="count!=0">#{count}</if>
                    <if test="state!=0">#{state}</if>
                </trim>
        )
    </insert>
```

## where标签

传入的用户对象，根据属性做where条件查询，用户对象中属性不为 null 的，都为查询条件。如
user.username 为 "a"，则查询条件为 where username="a"：
UserMapper 接口中新增条件查询方法：

```xml
<select id="selectByCondition" parameterType="org.example.model.User"
resultMap="BaseResultMap">
	select id, username, password, nickname, sex, birthday, head, create_time from user
    <where>
        <if test="username != null">
            and username=#{username}
        </if>
        <if test="password != null">
    		and password=#{password}
		</if>
		<if test="nickname != null">
    		and nickname=#{nickname}
		</if>
		<if test="sex != null">
    		and sex=#{sex}
        </if>
		<if test="birthday != null">
    		and birthday=#{birthday}
		</if>
		<if test="head != null">
   			and head=#{head}
		</if>
		<if test="createTime != null">
    		and create_time=#{createTime}
		</if>
		</where>
</select>
```

## set标签

<set>标签
根据传入的用户对象属性来更新用户数据，可以使用<set>标签来指定动态内容。
UserMapper 接口中修改用户方法：根据传入的用户 id 属性，修改其他不为 null 的属性：

```xml
<update id="updateById" parameterType="org.example.model.User">
	update user
	<set>
		<if test="username != null">
			username=#{username},
		</if>
		<if test="password != null">
			password=#{password},
		</if>
		<if test="nickname != null">
			nickname=#{nickname},
		</if>
		<if test="sex != null">
			sex=#{sex},
		</if>
		<if test="birthday != null">
			birthday=#{birthday},
		</if>
		<if test="head != null">
			head=#{head},
		</if>
		<if test="createTime != null">
			create_time=#{createTime},
		</if>
		</set>
		where id=#{id}
</update>
```

## foreach标签
对集合进行遍历时可以使用该标签。<foreach>标签有如下属性：
collection：绑定方法参数中的集合，如 List，Set，Map或数组对象
item：遍历时的每一个对象
open：语句块开头的字符串
close：语句块结束的字符串
separator：每次遍历之间间隔的字符串

```XML
<delete id="deleteByIds">
delete from article
where id in
	<foreach collection="list" item="item" open="(" close=")" separator=",">
		#{item}
	</foreach>
</delete>
```

