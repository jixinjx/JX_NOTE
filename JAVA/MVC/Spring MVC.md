# Spring MVC
Spring MVC框架设计图：
![[1661823381236.png]]
处理请求先到达控制器（ Controller ),控制器的作用是进行请求分发，这样它会根据请求的内容去访问模型层（ Model ）； 在现今互联网系统中，数据主要从数据库和NoSQL 中来，而且对于数据库而言往往还存在事务的机制，为了适应这样的变化，设计者会把模型层再细分为两层，即服务层（ Service ）和数据访问层（ DAO ） ； 当控制器获取到由模型层返回的数据后，就将数据渲染到视图中，这样就能够展现给用户了。
Spring MVC 全流程：
![[1661824030648.png]]

在Web 服务器启动的过程中，如果在Spring Boot 机制下启用Spring MVC ， 它就开始初
始化一些重要的组件，如DispactherS巳rvlet 、HandlerAdapter 的实现RequestMappingHandlerAdapter等组件对象。关于这些组件的初始化， 我们可以看到spring-webmvc-xxx.jar 包的属性文件DispatcherServ l et.propertion， 它定义的对象都是在SpringMVC 开始时就初始化，并且存放在Spring IoC容器中

这里的注解＠Controller 表明这是一个控制器，然后＠Re questMapping 代表请求路径和控制器（或其方法）的映射关系，它会在Web 服务器启动Spring MVC 时，就被扫描到Handler Mapping 的机制中存储，之后在用户发起请求被DispatcherServlet 拦截后，通过URL和其他的条件， 通过Ha ndlerMapper机制就能找到对应的控制器（或其方法）进行响应。只是通过HandlerMapping 返回的是一个HandlerExecutionChain 对象