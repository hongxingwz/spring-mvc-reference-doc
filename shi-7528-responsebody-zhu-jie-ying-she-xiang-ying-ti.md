# 使用@ResponseBody注解映射响应体(Mapping the response body with the @ResponseBody annotation)
`@ResponseBody`注解与`@RequestBody`注解很相似。此注解可以放在一个方法表示返回的类型应该直接写入到HTTP响应体(不要放置在Model中，或当作视图的名字拦截)。例如：


```
@GetMapping("/something")
@ResponseBody
public String helloWorld(){
    return "Hello World";
}
```
上述的例子将会造成文本`Hello World`直接被写入到HTTP响应流中。

像`@RequestBody`，Spring使用`HttpMessageConverter`将返回的对象转换成响应体中。要获取这些转换器更多的信息，参阅上一章节和[Message Converters](/Message Converters)

