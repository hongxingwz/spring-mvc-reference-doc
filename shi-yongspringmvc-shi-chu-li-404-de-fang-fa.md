# 使用springmvc时处理404的方法
## 如何定义404
404,说白了就是找不到页面，那么如何定义“找不到”呢？
我们可以通过源代码看看Spring MVC如何定义“404”的：

在DispatcherServlet中的doDispatch方法中有
```
// Determine handler for the current request.
	mappedHandler = getHandler(processedRequest);
	if (mappedHandler == null || mappedHandler.getHandler() == null) {			noHandlerFound(processedRequest, response);
			return;
    }
```

getHandler是根据请求的url，通过handleMapping来匹配到Controller的过程。
如果匹配不到，那么就执行noHandlerFound方法。这个方法很简单，返回一个404的错误代码。
我们的web容器，比如tomcat，会根据这个错误代码来生成一个错误界面给用户。
那么，我们如何定义这个界面呢？

##重写noHandlerFound方法
最先想到的肯定是重写noHandlerFound方法，这个方法是protected，可以重写

那么就自己定义一个MyDispatcherServlet类继承DispatcherServlet并重写noHandlerFound方法


```
    @Override
    protected void noHandlerFound(HttpServletRequest request, HttpServletResponse response) throws Exception {
        response.sendRedirect(request.getContextPath() + "/error.jsp");
    }
```
或者重定向到一个定义好的@Controller上


```
@Controller
@RequestMapping("/test/")
public class TestController {

    @RequestMapping("get3")
    @ResponseBody
    public String get3(HttpServletRequest request) {
        String contextPath = request.getContextPath();
        return contextPath + "/a/b/c";
    }
}
```

```
    @Override
    protected void noHandlerFound(HttpServletRequest request, HttpServletResponse response) throws Exception {
        response.sendRedirect(request.getContextPath() + "/test/get3");
    }
```





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

如


```
@Controller
public class ErrorController {

    @RequestMapping("/*")
    @ResponseBody
    public String get2() {
        return "/*";
    }

    @RequestMapping("/**")
    @ResponseBody
    public String get() {
        return "str str";
    }
}
```

会与下面的配置冲突


```
<mvc:resources mapping="/resources/**" location="/resources/"/>
```
在这里我不推荐使用




