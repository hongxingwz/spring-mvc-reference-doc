# 定义@RequestMapping注解的处理方法

使用@RequestMapping注解的处理方法可以拥有非常灵活的方法签名，它支持的方法参数及返回值类型将在接下来的小节讲述。大多数参数都可以任意的次序出现，除了唯一的一个例外：BindingResult参数。

> Spring3.1中新增了一些类，用以增强注解了@RequestMapping的处理方法，分别是RequestMappingHandlerMapping类和RequestMappingHandlerAdapter类。我们鼓励使用这组新的类，如果要使用Spring3.1及以后版本的新特性，这组类甚至是必须使用的。这些增强类在MVC的命名空间配置和MVC的Java编程方式配置中都是默认开启的，如果不是使用这两种方法，那么就需要显式地配置

## 支持的方法参数类型

下面列出所支持的方法参数类型：

* 请求或响应对象。可以是任何具体的请求或响应类型的对象，比如，**ServletRequest**或**HttpServletRequest**对象等。
* **HttpSession**类型的会话对象（Serlvet API\)。使用该类型的参数将要求这样一个**session**的存在，因此这样的参数永不为**null**

> 存取session可能不是线程安全的，特别是在一个Servlet的运行环境中。如果应用可能有多个请求同时并发存取一个session场景，请考虑将RequestMappingHandlerAdapter类中的”synchronizeOnSession“标志设置为"true"





