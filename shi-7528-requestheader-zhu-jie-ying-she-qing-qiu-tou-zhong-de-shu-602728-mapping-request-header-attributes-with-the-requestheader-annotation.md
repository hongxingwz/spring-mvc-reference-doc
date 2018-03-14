# 使用@RequestHeader注解映射请求头中的属性(Mapping request header attributes with the @RequestHeader annotation)

`@RequestHeader`注解允许方法参数绑定请求头的值

下面是一个简单的请求头

```
Host                    localhost:8080
Accept                  text/html,application/xhtml+xml,application/xml;q=0.9
Accept-Language         fr,en-gb;q=0.7,en;q=0.3
Accept-Encoding         gzip,deflate
Accept-Charset          ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Alive              300

```
下面的代码简单的展示了怎么获取头部`Accept-Encoding`和`Keep-Alive`的值



```
@RequestMapping("/displayHeaderInfo.do")
public void displayHeaderInfo(@RequestHeader("Accept-Encoding") String encoding,
        @RequestHeader("Keep-Alive") long keepAlive) {
    //...
}
```
类型转换会自动发生如果方法参数不是字符串，参阅[the section called "Method Parameters and Type Conversion"](/the section called "Method Parameters and Type Conversion")

当这个注解用于`Map<String, String>`, `MultiValueMap<String, String>` 或者 `HttpHeaders`参数时，map会被header中所有的值填充。



```
> 内置支持把由逗号分割的字符串转换成数组和集合或者其他被类型转换系统知道的类型。例如，一个被注解为`@RequestHeader("Accept")`参数的类型可以是`String`也可以是`String[]`或`List<String>`
```
此注解支持在Servlet和Portlet环境中的映射方法使用


