# 可消费的媒体类型

你可以指定一组可消费的媒体类型，缩小映射的范围。这样只有当请求头中_Content-Type_的值与指定可消费的媒体类型中有相同的时候，请求才会被匹配。请求才会被匹配。比如下面这个例子。

```
@Controller
@RequestMapping(path="/pets", consumes="application/json")
public void addPet(){
}
```

指定可消费媒体类型的表达式中，还可以使用否定，可以使用!text/plain来匹配所有请求头Context-Type中不含有text/plain的请求。

同时，在MediaType中还定义了一些常量，比如APPLICATION\_JSON\_VALUE 、APPLICATION_JSON_UTF8_VALUE等，推荐更多地使用它们。

> consumes属性提供的是方法级的类型支持。与其他属性不同，当在类级别使用时，方法级的消费类型将覆盖类级的配置。而非继承关系。

