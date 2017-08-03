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

如"/hotels/{hotel}/\*" 有一个URI变量和一个通配符 与 “/hotels/{hotel}/\*\*” 有一个URI变量和两个通配符。那么“/hotels/{hotel}/\*” 比

“/hotels/{hotel}/\*\*”更确切。

