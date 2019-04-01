#Spring
Spring 框架除了帮助我们管理对象之间的依赖关系，还提供像通用日志记录，性能统计，安全控制，异常处理等面向切面的能力，还能帮我们
管理最头疼的数据库事务，本身提供了一套简单的JDBC访问实现，提供于第三方数据库访问框架集成（如Hibernate，JPA），与各种Java EE 技术
整合（如JAVA mail,任务调度等等），提供一套自己的Web层框架Spring MVC、而且还能简单的与第三方Web框架继集成。从这里我们可以认为Spring
是一个超级粘合的大平台，除了自己提供的功能外，还提供粘合其他技术的框架能力。从而使我们可以更加自由的选择到底使用什么技术进行开发。
而且不管是JAVA SE（C/S架构）应用程序还是JAVA EE（B/S架构）应用程序都可以使用这个平台进行开发。如今的Spring已经不再是一个框架，早成为
了一种生态。SpringBoot 便捷式开发实现了零配置，SpringCloud 全家桶，提供了非常方便的解决方案，

## Spring 的设计初衷
1 基于POJO的轻量级和最小侵入性编程  
2 通过依赖注入和面向接口松耦合  
3 基于切面和惯性进行声明式编程  
4 通过切面和模板减少样板式代码  
主要是通过:面向Bean(BOP)\依赖注入（DI）、以及面向切面（AOP）这三种方式

## BOP编程
Spring 是面向Bean的编程（Bean Oriented Programming,BOP） Bean 在Spring中才是真正的主角。Spring提供了IOC容器通过配置文件或者注解的方式
来管理对象之间的依赖关系。  
控制反转：不创建对象，但是描述创建他们的方式，在代码中不直接与对象和服务连接，但是在配置文件中描述哪一个组件需要哪一项服务。容器负责
将这些联系在一起。  
在典型的IOC场景中，容器创建了所有对象，并设置必要的属性将他们连接在一起，决定什么时间调用方法。

### 依赖注入的基本概念  
Spring 设计的核心 org.springframework.beans 包（架构核心是org.springframework.core包），它的设计目标是与JavaBean组件一起使用，这个
包通常不是由用户直接使用，而是由服务器将其用作其他多数功能的底层中介。下一个最高级抽象是BeanFactory接口，它是工厂设计模式的实现，允许
通过名称创建和检索对象。BeanFactory也可以管理对象之间的关系。BeanFactory最底层支持两个对象模型。  
1 单例：提供了具有特定名称的全局共享实例对象，可以在查询时对其进行检索。Singleton 是默认的也是最常用的对象模型  
2 原型：确保每次检索都会创建单独的实例对象，在每个用户都需要自己的对象时，采用原型模式。
Bean工厂的概念时Spring作为IOC容器的基础，IOC 则将处理事情的责任从应用程序代码转移到框架。  

## AOP 编程理念
面向切面编程，即 AOP 是一种编程思想，它允许程序员对横切点和横切典型的职责分界线的行为（例如日志和事务管理）进行模块化。AOP的核心构造
是方面（切面），它将哪些影响多个类行为封装到可重用的模块中。  
AOP和IOC是补充性的技术，他们都运用模块化方式解决企业应用程序开发中的复杂问题。在典型的面向对象开发方式中，可能要将日志记录语句在所有
方法和java类中才能实现日志功能。在AOP方式中，可以反过来将日志服务模块化，并以声明的方式将他们应用到需要日志的组件上，当然，优势就是
Java类不需要知道日志服务的存在，也不需要考虑相关的代码。所以，用Spring AOP编写的应用程序代码是松耦合的。  
AOP的功能完全集成到了 Spring 的事务管理，日志和其他各种特性的上下文中  
AOP编程的常用场景：Authentication(权限认证)、AutoCaching(自动缓存处理)、Error Handing（统一错误管理）、Debugging(调试信息输出)、
Logging(日志记录)、Transactions(事务处理)等;  

## Spring5 系统架构
Spring 总共大约有20个模块，由1300多个不同的文件构成。而这个组件被分别整合在核心容器（Core Container）\AOP(Aspect Oriented Programming)
和设备支持（Instrmentation）、数据访问及集成（Data Access\Integeration）\Web \报文发送（Messaging）\test 6个模块集合中。
Spring5 的模块结构图：

### 核心容器
spring-core和spring-bean 模块是Spring 框架的核心模块，包含了控制反转和依赖注入。BeanFactory接口是Spring 框架中的核心接口，它是工厂
模式的具体实现。BeanFactory 使用控制反转实现对应用程序的配置和依赖性规范与实际的应用程序代码进行了分离。但是BeanFactory容器实例化
后并不会自动实例化Bean,只有当Bean被使用时 BeanFactory容器才会对该Bean 进行实例化与依赖关系的装配。  
Spring -Context 模块构架于核心模块之上，它扩展了BeanFactory 。为他添加了Bean的生命周期控制、框架事件体系以及资源加载透明化等功能。
此外该模块还提供了许多企业级支持，如邮件访问、远程访问、任务调度等，ApplicationContext 是该模块的核心接口，它的超类是BeanFactory。
与BeanFactory 不同，ApplicationContext 容器实例化后会自动对所有的单实例Bean 进行实例化与依赖关系的装配，使之处于待用状态。  
spring-context-support:模块是对Spring IOC容器的扩展支持，以及IOC子容器。  
spring-context-indexer:模块是Spring 的类管理组件和ClassPath扫描。  
spring-expression: 模块是统一表达式语言EL 的扩展模块，可以查询、管理运行中的对象，同时也方便的可以调用对象方法、操作数组、集合等。 
它的语法类似于传统的EL，但是提供了额外的功能，最出色的要数函数调用和简单字符串的模板函数。这种语言的特性是基于Spring产品的需求设计
它可以非常方便地通Spring IOC进行交互。  

### AOP和设备支持  
由spring-aop spring-aspects 和 spring - instrument 3个模块组成。  
spring-aop 是Spring 地另一个核心模块，是AOP  主要地实现模块。作为继OOP后，对程序员影响最大地编程思想之一，AOP极大的开拓了人们对于编程
地思路。在Spring中，它是以JVM地动态代理技术为基础，然后设计了一系列AOP横切实现，比如前置通知、返回通知、异常通知等，同时，Pointcut
接口来匹配切入点，可以使用现有地切入点来设计横切面，也可以扩展相关方法根据需求进行切入。  
spring-aspects 模块集成自AspectJ框架，主要是为Spring AOP提供多种AOP实现方法。  
spring-instrument 模块是基于JAVA SE中地 java.lang.instrument 进行设计地，应该算是AOP地一个支援模块，主要作用是在JVM启用时，生成一个
代理类，程序员通过代理类在运行时修改类地字节，从而改变一个类地功能，实现AOP地功能。

### 数据访问和集成
由Spring - jdbc spring-tx spring-orm spring-jms spring-oxm 5个模块组成  
spring-jdbc 模块是Spring 提供地JDBC抽象框架地主要实现模块，用于简化spring JDBC 操作。主要是提供JDBC模板方式、关系数据库对象化方式、
SimpleJdbc方式、事务管理来简化JDBC编程，主要实现类JdbcTemplate\SimpleJdbcTemplate\NamedParameterJdbcTemplate.  
spring-tx 模块是Spring JDBC事务控制实现模块，使用Spring 框架，它对事务做了很好地封装，通过它地AOP配置，可以灵活地配置任何一层；但是
在很多地需求和应用，直接使用JDBC事务控制还是有其优势地，。其实，事务是以业务逻辑为基础地，一个完整地业务应该对业务层里地一个方法。
如果业务操作失败，则整个事务回滚，所以，事务控制是绝对应该放在业务层里地，但是，持久层地设计则应该遵循一个很重要地原则：保证操作地
原子性，即持久层里地每个方法都应该是不可以分割地，所以，在使用Spring JDBC事务控制时，应该注意其特殊性。  
spring-orm模块时ORM框架支持模块，主要集成Hibernate,Java Persistence API(JPA) 和 java data Objects(JDO) 用于资源管理、数据访问对象
DAO 地实现和事务策略。  
spring-oxm模块主要提供一个抽象层以支撑 OXM（OXM Object - To -XML-Mapping 地缩写），它是一个O/M-mapper ,将Java 对象映射成XML数据，
或者将XML数据映射成JAVA对象。 例如JAXB Castor XMLBeans JiBX 和 XStream等
spring--jms 模块（JAVA Messaging service）能够发送和接收信息，自Spring Framework4.1 以后，还提供了spring-messaging 模块地支撑。  

### Web组件  
由spring-web spring-webmvc spring-websocket 和 spring-webflux 4个模块组成  
spring-web 模块为spring 提供了最基础地Web支持，主要建立于核心容器之上，通过servlet 或者Listeners 来初始化IOC容器，也包含一些Web相关
地支持。  
spring-webmvc 模块众所周知是一个Web-Servlet 模块，实现了Spring MVC（model-view-Controller）地Web应用。  
spring-websocket 模块主要是与web前端地全双工通讯地协议。  
spring-webflux 是一个新的非阻塞函数式 Reactive Web框架，可以用来建立异步地，非阻塞，事件驱动地服务，并且扩展性非常号。  

### 通信报文  
即Spring-messaging 模块，是从Spring4 开始新加入地一个模块，主要职责是为Spring框架集成一些基础地报文传送应用。  

### 集成测试 
spring-test 模块，主要为测试提供支持地，毕竟在不需要发布（程序）到你地应用服务器或者连接到其他企业设置地情况下能够执行一些集成测试
或者 其他测试对于任何企业都是非常重要地。  

### 各个模块之间地依赖关系  

### Spring 版本命名规则
X.Y.Z(Major.Minor.Patch)  
X 非负整数  表示主版本号，当API 的兼容性发生变化时，X需要递增
Y 非负整数  表示次版本号，当增加功能时（不影响API的兼容性），Y需要递增
Z 非负整数  表示修订号，当做bug修复时（不影响API的兼容性）,Z需要递增

Snapshot 快照版  尚不稳定，尚处于开发中的版本  
Release  稳定版  功能相对稳定，可以对外发行，但是又时间限制  
GA       正式版  代表广泛可用的稳定版  
M        里程碑版  M是Milestone 的意思  具有一些全新的功能或是具有里程碑意义的版本。  
RC       终测版    Release Candidate 最终测试，即将作为正式版发布。  
