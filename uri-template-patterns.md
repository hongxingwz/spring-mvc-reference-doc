# URI Template Patterns

A URI Template is a URI-like string

```
@GetMapping("/onwers/{ownerId}")
public String findOwner(@PathVairable String ownerId){

}
```

一个方法可以有任意数量的@PathVariable注解

```
@GetMapping("/owners/{ownerId}/pets/{petId}")
public String findPet(@PathVariable String ownerId, @PathVariable String petId){

}
```

## URI Template Patterns with Regular Expressions

@RequestMapping注解支持在URI模板变量中使用正则表达式。

语法是{varName:regex}：第一部分定义了变量的名字，第二部分定义了正则表达式

如像"/spring-web/spring-web-3.0.5.jar"

```
@RequestMapping("/spring-web/{symbolicName:[a-z-]+}-{version:\\d\\.\\d\\.\\d}{extension:\\.[a-z]+}")
public void handle(@PathVariable String version, @PathVariable String extension){
..
}
```

## Path Patterns

**也支持Ant-Sytle path patterns: **\(例如: /myPath/\*.do\)

**URI模板变量和Ant-style 相结合也是支持的**

```
@RequestMapping("/owners/*/pets/{petId}")
```

### Path Pattern Comparison

当一个URL匹配到多个模式时，会选择使用最确切的那一个

* 如"/hotels/{hotel}/\*" 有一个URI变量和一个通配符 与 “/hotels/{hotel}/\*\*” 有一个URI变量和两个通配符。那么“/hotels/{hotel}/\*” 比“/hotels/{hotel}/\*\*”更确切。

* 如果两个匹配模式的数量是一样的，那么更长的那个认为是最准确的。例如/foo/bar\*比/foo/\*更长，被认为是最准确的
* 当两个匹配模式具有一样的数量和长度，具有更少通配符的那个模式被认为是更确切的。例如：/hotels/{hotel}比/hotels/\*更准确。

### Path Patterns with Placeholders

@RequestMapping注解中的匹配模式支持**${...}**占位符（本地和系统属性和环境变量）

这可能对映射到的路径可能需要配置文件配置 这种情况来说非常有用



