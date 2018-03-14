# 可生产的媒体类型(Producible Media Types)
你可以通过指定一系列的可生产的媒体类型来缩小主映射类型的范围。仅当请求头的`Accept`与指定的值相匹配映射才会匹配。而且，使用produces条件保证了生成的响应头的`Content-Type`包含了指定的。例如


```
@GetMapping(path = "/pets/{petId}", produces = MediaType.APPLICATION_JSON_UTF8_VALUE)
@ResponseBody
public Pet getPet(@PathVariable String petId, Model model) {
    // implementation omitted
}
```

> 要注意到指定的可生产的媒体类型也可以指定字符集。例如，在上面的代码片断中，我们指定了一样的媒体类型而不是在
`MappingJackson2HttpMessageConverter`中配制的默认的媒体类型，包括`UTF-8`字符集

和可消费的媒体类型一样，可生产的媒体类型表达式可以像`!text/plain`取反来匹配请求头中`Accept`的值不是`text/plain`的。可以考虑使用由`MediaType`提供的常量如`APPLICATION_JSON_VALUE`和`APPLICATION_JSON_UTF8_VALUE`

> 消费条件同时被类型和方法级别支持。不像大多数其他的条件，当同时在类型和方法级别使用时，方法级别会覆盖类型级别的而不是继承类型级别


