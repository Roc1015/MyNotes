# SpringFamily











































## SpringCloud

注：

- 官方网站：https://spring.io/projects/spring-cloud
- 中文学习网站：https://www.springcloud.cc/
- 快速开始：https://www.springcloud.cc/spring-cloud-config.html#_quick_start
- 截止2021.01.11，SpringCloud更新到2020.0.0

### 一.什么是SpringCloud

![image-20210111172450774](../imgs/image-20210111172450774.png)

```xml
	Spring Cloud为开发人员提供了快速构建分布式系统中的一些常见模式的工具(例如配置管理、服务注册与发现、断路器、智能路由、微代理、控制总线、一次性令牌、全局锁、领导人选举、分布式会话、集群状态)。分布式系统的协调导致了锅炉板模式，而使用Spring Cloud开发人员可以快速建立实现这些模式的服务和应用程序。它们在任何分布式环境中都能很好地工作，包括开发人员自己的笔记本电脑、裸金属数据中心和云计算等托管平台。
```



### 二.为什么用SpringCloud

#### 1.SpringCloud和SpringBoot的关系

```xml
1. SpringBoot专注于开发方便的开发单个个体微服务；SpringCloud是关注全局的微服务协调整理治理框架，它将SpringBoot开发的一个个单体微服务，整合并管理起来，为各个微服务之间提供：配置管理、服务发现、断路器、路由、为代理、事件总栈、全局锁、决策竞选、分布式会话等等集成服务；
2. SpringBoot可以离开SpringCloud独立使用，开发项目，但SpringCloud离不开SpringBoot，属于依赖关系
```

2.什么是微服务？

```xml
微服务是指具体解决某一个问题/提供落地对应服务的一个服务应用，狭义的看，可以看作是IDEA中的一个个微服务工程，或者Moudel。
```

3.微服务与微服务架构

```xml
通常而言，微服务架构是一种架构模式，或者说是一种架构风格，它体长将单一的应用程序划分成一组小的服务，每个服务运行在其独立的自己的进程内，服务之间互相协调，互相配置，为用户提供最终价值，服务之间采用轻量级的通信机制(HTTP)互相沟通，每个服务都围绕着具体的业务进行构建，并且能狗被独立的部署到生产环境中，另外，应尽量避免统一的，集中式的服务管理机制，对具体的一个服务而言，应该根据业务上下文，选择合适的语言，工具(Maven)对其进行构建，可以有一个非常轻量级的集中式管理来协调这些服务，可以使用不同的语言来编写服务，也可以使用不同的数据存储。
```

4.微服务的优缺点

```xml
优点：
1.	单一职责原则；
2.	每个服务足够内聚，足够小，代码容易理解，这样能聚焦一个指定的业务功能或业务需求；
3.	开发简单，开发效率高，一个服务可能就是专一的只干一件事；
4.	微服务能够被小团队单独开发，这个团队只需2-5个开发人员组成；
5.	微服务是松耦合的，是有功能意义的服务，无论是在开发阶段或部署阶段都是独立的；
6.	微服务能使用不同的语言开发；
7.	易于和第三方集成，微服务允许容易且灵活的方式集成自动部署，通过持续集成工具，如jenkins，Hudson，bamboo；
8.	微服务易于被一个开发人员理解，修改和维护，这样小团队能够更关注自己的工作成果，无需通过合作才能体现价值；
9.	微服务允许利用和融合最新技术；
10.	微服务只是业务逻辑的代码，不会和HTML，CSS，或其他的界面混合;
11.	每个微服务都有自己的存储能力，可以有自己的数据库，也可以有统一的数据库；

缺点：
1.	开发人员要处理分布式系统的复杂性；
2.	多服务运维难度，随着服务的增加，运维的压力也在增大；
3.	系统部署依赖问题；
4.	服务间通信成本问题；
5.	数据一致性问题；
6.	系统集成测试问题；
7.	性能和监控问题；
```

5.微服务技术栈

![image-20210112100750179](../imgs/image-20210112100750179.png)

6.dubbo和SpringCloud

### 三.SpringCloud

#### 1.SpringCloud版本选择

- 采用伦敦地铁站进行版本区分，推荐使用GA稳定版本（截止2021.01.12，版本更新到2020.0.0）

![image-20210112105714367](../imgs/image-20210112105714367.png)

#### 2.SpringCloud快速开始

- 快速开始：https://www.springcloud.cc/spring-cloud-config.html#_quick_start

#### 3.新建SpringCloud

- maven依赖导入

```xml
<!---->
<dependency>
    <groupId></groupId>
    <artifactId></artifactId>
    <version></version>
</dependency>
```

```xml
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <lomok.version>1.18.16</lomok.version>
    </properties>

    <!--打包方式-->
    <!--注：版本截止到2021.01.12-->
    <packaging>pom</packaging>

    <dependencyManagement>
        <dependencies>

            <!--SpringCloud依赖-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Hoxton.SR1</version>
                <type>pom</type>
            </dependency>

            <!--SpringBoot-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.4.1</version>
            </dependency>

            <!--SpringBoot启动器-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter</artifactId>
                <version>2.4.1</version>
            </dependency>

            <!--数据库-->
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>5.1.38</version>
            </dependency>

            <!--数据源-->
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>1.1.23</version>
            </dependency>

            <!--myBatis-->
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>2.1.4</version>
            </dependency>

            <!--log4j-->
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>1.2.17</version>
            </dependency>

            <!--junit-->
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.13.1</version>
                <scope>test</scope>
            </dependency>

            <!--lombok-->
            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>${lomok.version}</version>
            </dependency>

        </dependencies>
```

- 方便依赖导入版本维护

![image-20210112152043199](../imgs/image-20210112152043199.png)

![image-20210112152056068](../imgs/image-20210112152056068.png)





















































