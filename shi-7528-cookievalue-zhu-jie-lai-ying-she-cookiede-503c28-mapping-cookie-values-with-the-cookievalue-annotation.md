# 使用@CookieValue注解来映射cookie的值(Mapping cookie values with the @CookieValue annotation)

`@CookieValue`注解允许一个方法参数绑定到HTTP cookie值
让我们想像一下，你面这条cookie值从一个http请求中接收到

```
JSESSIONID=415A4AC178C59DACE0B2C9CA727CDD84
```
下面的代码展示了怎么获取cookie中JESSIONID的值


```
@RequestMapping("/displayHeaderInfo.do")
public void displayHeaderInfo(@CookieValue("JSESSIONID") String cookie) {
    //...
}
```
类型转换会自动适用如果目标方法参数的类型不是`String`. 参阅[the section called "Method Parameters And Type Conversion"](/the section called "Method Parameters And Type Conversion")

此注解在Servlet和Portlet环境下被支持

