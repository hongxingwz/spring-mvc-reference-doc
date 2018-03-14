# 可消费的媒体类型(Consumable Media Types)
你可以通过指定一系列的可消费的媒体类型类缩小主映射(primary mapping)的范围。仅当请求的请求头中的`Content-Type`与指定的媒体类型相匹配，映射才会匹配。例如：

```
@PostMapping(path = "/pets", consumes = "application/json")
public void addPet(@RequestBody Pet pet, Model model) {
    // implementation omitted
}
```
可消费媒体类型的表达式也可以是否定的`!text/plain`来匹配所有`Content-Type`不是`text/plain`的请求。可以考虑使用由`MediaType`提供的常量如`APPLICATION_JSON_VALUE`和`APPLICATION_JSON_UTF8_VALUE`

> 消费条件同时被类型和方法级别支持。不像大多数其他的条件，当同时在类型和方法级别使用时，方法级别会覆盖类型级别的而不是继承类型级别

