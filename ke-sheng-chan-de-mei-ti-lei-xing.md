# 可生产的媒体类型

你可以指定一组可生产的媒体类型，缩小映射的范围。这样只有当请求头中**Accept**的值与指定可生产的媒体类型中有相同的时候，请求才会被匹配。而且，使用produces条件可以确保用于生成响应\(reponse\)的内容与指定的可生产的媒体类型是相同的。举个例子：

```
@Controller
@RequestMapping(path="/pets/{petId}", 
    method=RequestMethod.GET, produces=MediaType.APPLICATION_JSON_UTF8_VALUE)
@ResponseBoby
public Pet getPet(@PathVariable String petId, Model model){
    //方法实现省略
}
```

与consumes条件类似，可生产的媒体类型表达式也可以使用否定。比如，可以使用!text/plain来匹配所有请求头Accept中不含text/plain的请求。同时，在MediaType类中还定义了一些常量，比如APPLICATION\_JSON\_\VALUE, APPLICATION\_JSON\_UTF8\_VALUE等，推荐更多地使用它们。

