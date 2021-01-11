## spring

### 一.spring

### 二.spring boot：https://spring.io/projects/spring-boot

#### 1.原理

pom.xml：

* maven：导入组件的jar包
* 启动器：

```xml
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.0</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
```

* 主程序：

```java
@SpringBootApplication
public class ForceApplication {
    public static void main(String[] args) {
        SpringApplication.run(ForceApplication.class, args);
    }
}
```

#### 2.application.yaml/application.properties

yaml语法结构：key： Value（对空格要求极高）

properties语法结构：key=Value

![image-20201221152849075](..\image-20201221152849075.png)



通过yaml注入对象：

person类：

```java
@Component
@ConfigurationProperties(prefix = "person")
//添加@ConfigurationProperties注解，且绑定person类
public class Person {
    private String name;
    private Integer age;
    private Boolean happy;
    private Date brith;
    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
```

application.yaml：

```xml
person:
  name: wangpeng
  age: 23
  happy: false
  brith: 1997/10/15
  maps: {k1: v1,k2: v2}
  lists:
    -code
    -music
  dog:
    name: wangcai
    age: 3
```

test类：

```java
@SpringBootTest
class Force001ApplicationTests {

    //注入person类
    @Autowired
    Person person;

    @Test
    void contextLoads() {
        System.out.println(person);
    }
}
```

输出结果：

![image-20201221165734041](C:\Users\魁\Desktop\force\图片\image-20201221165734041.png)

注：实体类与yaml绑定时出错爆红，缺少依赖：引入依赖/忽略爆红，直接绑定

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <version>2.4.0</version>
            <optional>true</optional>
        </dependency>
```



![image-20201221170236134](C:\Users\魁\Desktop\force\图片\image-20201221170236134.png)

yaml注入对象的用处

* 可与全局配置类结合进行全局配置
* 多份配置文件亦可通过注解@PropertySource(value = "classpath:***.properties")进行自定义

#### 3.JSR303校验

通过注解@Validated实现：https://www.cnblogs.com/liaojie970/p/9036349.html

导入注解：

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
            <version>2.4.1</version>
        </dependency>
```

在类上添加@vaildated注解，在详细的字段上添加相应的校验

```xml
@AssertFalse 校验false
@AssertTrue 校验true
@DecimalMax(value=,inclusive=) 小于等于value，
inclusive=true,是小于等于
@DecimalMin(value=,inclusive=) 与上类似
@Max(value=) 小于等于value
@Min(value=) 大于等于value
@NotNull  检查Null
@Past  检查日期
@Pattern(regex=,flag=)  正则
@Size(min=, max=)  字符串，集合，map限制大小
@Validate 对po实体类进行校验
```

![image-20201222095131558](C:\Users\魁\Desktop\force\图片\image-20201222095131558.png)

@Pattern正则表达式：

![image-20201222100445082](C:\Users\魁\Desktop\force\图片\image-20201222100445082.png)

常用的正则表达式：

```xml
  1 匹配首尾空格的正则表达式：(^\s*)|(\s*$)
  2 整数或者小数：^[0-9]+\.{0,1}[0-9]{0,2}$
  3 只能输入数字："^[0-9]*$"。
  4 只能输入n位的数字："^\d{n}$"。
  5 只能输入至少n位的数字："^\d{n,}$"。
  6 只能输入m~n位的数字：。"^\d{m,n}$"
  7 只能输入零和非零开头的数字："^(0|[1-9][0-9]*)$"。
  8 只能输入有两位小数的正实数："^[0-9]+(.[0-9]{2})?$"。
  9 只能输入有1~3位小数的正实数："^[0-9]+(.[0-9]{1,3})?$"。
 10 只能输入非零的正整数："^\+?[1-9][0-9]*$"。
 11 只能输入非零的负整数："^\-[1-9][]0-9"*$。
 12 只能输入长度为3的字符："^.{3}$"。
 13 只能输入由26个英文字母组成的字符串："^[A-Za-z]+$"。
 14 只能输入由26个大写英文字母组成的字符串："^[A-Z]+$"。
 15 只能输入由26个小写英文字母组成的字符串："^[a-z]+$"。
 16 只能输入由数字和26个英文字母组成的字符串："^[A-Za-z0-9]+$"。
 17 只能输入由数字、26个英文字母或者下划线组成的字符串："^\w+$"。
 18 验证用户密码："^[a-zA-Z]\w{5,17}$"正确格式为：以字母开头，长度在6~18之间，只能包含字符、数字和下划线。
 19 验证是否含有^%&',;=?$\"等字符："[^%&',;=?$\x22]+"。
 20 只能输入汉字："^[\u4e00-\u9fa5]{0,}$"
 21 验证Email地址："^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$"。
 22 验证InternetURL："^http://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$"。
 23 验证电话号码："^(\(\d{3,4}-)|\d{3.4}-)?\d{7,8}$"正确格式为："XXX-XXXXXXX"、"XXXX-XXXXXXXX"、"XXX-XXXXXXX"、"XXX-XXXXXXXX"、"XXXXXXX"和"XXXXXXXX"。
 24 验证身份证号（15位或18位数字）："^\d{15}|\d{18}$"。
 25 验证一年的12个月："^(0?[1-9]|1[0-2])$"正确格式为："01"～"09"和"1"～"12"。
 26 验证一个月的31天："^((0?[1-9])|((1|2)[0-9])|30|31)$"正确格式为；"01"～"09"和"1"～"31"。
 27 匹配中文字符的正则表达式： [\u4e00-\u9fa5]
 28 匹配双字节字符(包括汉字在内)：[^\x00-\xff]
 29 应用：计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）
 30 String.prototype.len=function(){return this.replace(/[^\x00-\xff]/g,"aa").length;}
 31 匹配空行的正则表达式：\n[\s| ]*\r
 32 匹配html标签的正则表达式：<(.*)>(.*)<\/(.*)>|<(.*)\/>
```

#### 4.多环境配置及配置文件位置

![image-20201222102639661](C:\Users\魁\Desktop\force\图片\image-20201222102639661.png)

海外艾玛项目：

![image-20201222103446476](C:\Users\魁\Desktop\force\图片\image-20201222103446476.png)

#### 5.Spring Web

test：hello，world

```xml
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello(){
        return "hello,world";
    }
}
```

##### 1.**restful风格**

##### 2.处理静态资源：···/ico

##### 3.Thymleaf模板引擎

Thymleaf官网：https://www.thymeleaf.org/

Thymleaf学习博客：https://www.cnblogs.com/msi-chen/p/10974009.html#_label0

引入依赖：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

##### 4.MVC









































































