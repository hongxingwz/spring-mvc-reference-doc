# 使用springmvc时处理404的方法

## 利用web容器提供的error-page

还记得之前提到的web容器会提供一个404的默认界面吗？  
其实我们完全可以替换成我们自己的界面，那么看起来这种方法应该是最简单的了。  
只需要在web.xml文件中写上如下代码就可以了

```
<error-page>
    <error-code>404</error-code>
    <location>/error.jsp</location>
</error-page>
```

> 注：/error.jsp 这个资源文件一定要以/开头要不然tomcat会报错，并启动不起来



~~注：这里配置的location其实会被当成一个请求来访问。那么我们的DispatcherServlet会拦截这个请求而造成无法访问，此时的结果是用户界面一片空白。所以这里的404.htm其实是一个静态资源，我们需要访问静态资源的方式去访问。~~

实际上DispatcherServlet不会拦截，因为当返回404的错误时，实际上是由tomcat在次重定向到配置的&lt;location&gt;...&lt;location&gt;的资源的。

如配置成如下

```
<error-page>
    <error-code>404</error-code>
    <location>/WEB-INF/jsp/manage/footer.jsp</location>
 </error-page>
```

访问一个不存在的资源时得到如下的页面

![](/assets/1511743094799.png)

## 利用Spring Mvc的最精确匹配

Spring MVC对于url的匹配采用的是一种叫做“最精确匹配的方式”，举个例子

比如我们同时定义了“/test/a”, "/test/\*", 那么若请求的url结尾是"/test/a",那么则会匹配精确的那个，也就是"/test/a"

我们是不是可以利用这个特点来找到那此找不到的页面？

* 首先我们定义一个拦截所有url的规则@RequestMapping("*"),那么实际不存在找不到的页面了，也就是永远不会进入noHandlerFound方法体内
* 后面的步骤和平时一样，为别的请求配置上@RequestMapping
那么请求过来，要么进入我们精确匹配的method(也就是找到的），要么进入@RequestMapping("*")拦截的方法体内(也就是找不到的)



