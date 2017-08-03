# Binding request parameters to method parameters with @RequestParam

用@RequestParam注解，把请求参数绑定到方法参数。

```java
@Target(ElementType.PARAMETER)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface RequestParam{

    @AliasFor("name")
    String value() default "";

    @AliasFor("value")
    String name() default "";

    boolean required() default true;

    String defaultValue() default ValueConstants.DEFAULT_NONE;
```

* 参数使用此注解默认是**必须**的，但你可以指定一个可选的参数通过设置@RequestParam的required属性等于false（e.g., @RequestParam\(name="id", required=false\)

> 注：当设置了@RequestParams的defaultValue属性时，则参数也是可选的。（e.g., @RequestParam\(name="id", defaultValue="-1"\) 这样请求时不传入id参数，也不会报错





* 类型转换自动运行当目标参数类型不是一个字符串时。看 the section called "Method Parameters And Type Conversion".







* 当一个@RequestParam注解用在一个Map&lt;String, String&gt;或者MultiValueMap&lt;String, String&gt;参数上时，map会填充所有的请求参数。

**Map&lt;String, String&gt;**

```java
@RequestMapping("map")
@ResponseBody
public String map(@RequestParam Map<String, String> map) {
    return map.toString();
}

/*
请求：http://localhost:8082/pig/map?name=jianglei&age=18&love=dengyi&a=1&b=2&c=3&c=9
返回：{name=jianglei, age=18, love=dengyi, a=1, b=2, c=3}

*/
```

**MultiValueMap&lt;String, String&gt;**

```java
@RequestMapping("multiMap")
@ResponseBody
public String multiMap(@RequestParam MultiValueMap<String, String> multiValueMap) {

    return multiValueMap.toString();
}
/*
请求：http://localhost:8082/pig/map?name=jianglei&age=18&love=dengyi&a=1&b=2&c=3&c=9
返回：{name=[jianglei], age=[18], love=[dengyi], a=[1], b=[2], c=[3, 9]}
*/
```



