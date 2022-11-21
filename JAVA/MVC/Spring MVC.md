# Spring MVC
Spring MVC框架设计图：
![[1661823381236.png]]
处理请求先到达控制器（ Controller ),控制器的作用是进行请求分发，这样它会根据请求的内容去访问模型层（ Model ）； 在现今互联网系统中，数据主要从数据库和NoSQL 中来，而且对于数据库而言往往还存在事务的机制，为了适应这样的变化，设计者会把模型层再细分为两层，即服务层（ Service ）和数据访问层（ DAO ） ； 当控制器获取到由模型层返回的数据后，就将数据渲染到视图中，这样就能够展现给用户了。
Spring MVC 全流程：
![[1661824030648.png]]


- 用户发送请求至前端控制器DispatcherServlet
- DispatcherServlet收到请求调用HandlerMapping处理器映射器。
- 处理器映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。
- DispatcherServlet通过HandlerAdapter处理器适配器调用处理器
- 执行处理器(Controller，也叫后端控制器)。
- Controller执行完成返回ModelAndView
- HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet
- DispatcherServlet将ModelAndView传给ViewReslover视图解析器
- ViewReslover解析后返回具体View
- DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）。
- DispatcherServlet响应用户。

在Web 服务器启动的过程中，如果在Spring Boot 机制下启用Spring MVC ， 它就开始初
始化一些重要的组件，如DispactherS巳rvlet 、HandlerAdapter 的实现RequestMappingHandlerAdapter等组件对象。关于这些组件的初始化， 我们可以看到spring-webmvc-xxx.jar 包的属性文件DispatcherServ l et.propertion， 它定义的对象都是在SpringMVC 开始时就初始化，并且存放在Spring IoC容器中



这里的注解＠Controller 表明这是一个控制器，然后＠RequestMapping 代表请求路径和控制器（或其方法）的映射关系，它会在Web 服务器启动Spring MVC 时，就被扫描到Handler Mapping 的机制中存储，之后在用户发起请求被DispatcherServlet 拦截后，通过URL和其他的条件，通过Ha ndlerMapper机制就能找到对应的控制器（或其方法）进行响应。只是通过HandlerMapping 返回的是一个HandlerExecutionChain 对象

HandlerExecutionChain 对象包含一个处理器（ handler ） 。这里的处理器是对控制器（ controller ）的包装，因为我们的控制器方法可能存在参数，那么处理器就可以读入HTTP和上下文的相关参数，然后再传递给控制器方法。而在控制器执行完成返回后，处理器又可以通过配置信息对控制器的返回结果进行处理。从这段描述中可以看出，处理器包含了控制器方法的逻辑，此外还有处理器的拦截器（ interceptor ），这样就能够通过拦截处理器进一步地增强处理器的功能。

得到了处理器（ handler ），还需要去运行，但是我们有普通HTTP 请求，也有按BeanName 的请
求，甚至是WebSocket 的请求，所以它还需要一个适配器去运行HandlerExecutionChain 对象包含的处理器，这就是HandlerAdapter 接口定义的实现类。在代码清单9-1 中，我们可以看到在Spring MVC中最常用的HandlerAdapter 的实现类，这便是HttpRequestHandlerAdapter o 通过请求的类型，DispatcherServlet 就会找到它来执行Web 请求的HandlerExecutionChain 对象包含的内容，这样就能够执行我们的处理器（ handler ）了。
在处理器调用控制器时，它首先通过模型层得到数据，再放入数据模型中，最后将返回模型和视图（ ModelAndView ）对象，这里控制器设置的视图名称设置为“user/details ”，这样就走到了视图解析器（ ViewResolver ），去解析视图逻辑名称了。