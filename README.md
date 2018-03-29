# web
study web 

This is not good.


```text
Tomcat启动
/WEB-INF/web.xml是Servlet规范的部署描述符，它描述了如何在一个Servlet容器中部署一个web应用，包括：session配置、servlet配置和映射、filter配置和映射、监听应用生命周期的listener、首页和错误页面配置、安全配置等。
同时，Servlet 3.0提供了web模块化规范，部署描述符也可以存在于/WEB-INF/lib/**.jar/web-fragment.xml中，并在web应用部署时解析。
另外，Tomcat提供了全局web.xml：$CATALINA_BASE/conf/web.xml。与web-fragment一样的是，其配置将与web.xml合并，顺序可以通过ordering标签配置，具体合并规则见Servlet 3.0标准8.2.3节。
解析web.xml的过程就是读取各种部署描述符文件，合并并应用到容器中的过程，大体过程如下：

- 使用WebXmlDigester，将web.xml的数据解析到WebXml对象中
- 扫描/WEB-INF/lib下每个Jar包内的/META-INF/web-fragment.xml并解析，根据一定的规则排序，并放入Set中
- 扫描/WEB-INF/lib下每个Jar包内的/META-INF/services/目录下的ServletContainerInitializer实现类，放入StandardContext.initializers中（后续将执行其onStartup方法）
- 扫描/WEB-INF/classes下的servlet注解并添加相应配置
- 将第一步解析的应用web.xml和第二步解析的web-fragment.xml以及全局的web.xml文件(conf/web.xml 、web.xml.default)合并到WebXml对象中
- 将合并后的WebXml配置到Context中，例如为每个Servlet创建Wrapper并作为Context的子容器

Tomcat启动时会扫描/WEB-INF/lib下每个Jar包内的/META-INF/services/目录下的ServletContainerInitializer实现类，放入StandardContext.initializers中（后续将执行其onStartup方法）。spring-web包扩展了这个特性，增加了SpringServletContainerInitializer类，重写的onStartUp方法会执行所有WebApplicationInitializer的onStartup方法。
spring-web包扩展了这个特性，增加了SpringServletContainerInitializer类，重写的onStartUp方法会执行所有WebApplicationInitializer的实现的onStartup方法。
spring-boot包定义了SpringBootServletInitializer抽象类，重写了onStartup方法，这样就桥接到Spring Boot的启动了。


Spring Boot启动

SpringBootServletInitializer  run
创建应用上下文，初始化应用ApplicationBuilder，调用定制的configure方法，最后执行run，初始化spring-context

SpringApplication  run->refreshContext->refresh

EmbeddedWebApplicationContext  refresh

AbstractApplicationContext   refresh -> registerBeanPostProcessors

PostProcessorRegistrationDelegate  registerBeanPostProcessors

AbstractBeanFactory  getBean   ->  doGetBean

DefaultSingletonBeanRegistry  getSingleton

AbstractBeanFactory   getObject

AbstractAutowireCapableBeanFactory  createBean -> doCreateBean -> createBeanInstance -> instantiateUsingFactoryMethod

ConstructorResolver  instantiateUsingFactoryMethod  ->  createArgumentArray  ->  resolveAutowiredArgument

DefaultListableBeanFactory   resolveDependency  ->  doResolveDependency



```
