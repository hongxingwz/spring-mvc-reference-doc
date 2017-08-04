# 后缀模式匹配

Spring MVC 默认采用“.\*”的后缀模式匹配来进行路径匹配，因此，一个映射到/person路径的控制器也会隐式地映射到/person.\*。这使用通过URL来请求同一资源文件的不同格式变得更简单\(比如/person.pdf, /person.xml\)



你可以关闭默认的后缀模式匹配，或者显式地将路径后缀限定到一些特定格式上。我们推荐这样做，这样可以减少映射请求时可以带来的一些二义性，比如请求以下路径/person/{id}时，路径中的点号后面带的可能不是描述内容格式,比如/person/joe@email.com vs /person/joe@email.com.json。而且正如下面马上要提到的，后缀模式通过以及内容协商有时可能会被黑客用来进行攻击，因此，对后缀通配进行有意义的限定是有好处的。



**关闭默认的后缀模式匹配**

* java方式

```java
    @Bean
    public RequestMappingHandlerMapping mapping() {
        RequestMappingHandlerMapping mapping = new RequestMappingHandlerMapping();
        mapping.setUseSuffixPatternMatch(true);

        return mapping;
    }
```

* xml方式

```xml
<mvc:annotation-driven>
    <mvc:path-matching suffix-pattern="false"/>
</mvc:annotation-driven>
```



