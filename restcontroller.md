@RestController

一个方便的注解自身由注解@Controller和@ResponseBody标注

携带此注解的类型被视为一个controller  带有@RequestMapping注解的方法也会具有@ResponseBody

> 注：@RestController会被处理如果一个适当的@HandlerMapping和@HandlerAdapter配置成RequestMappingHandlerMapping 和 RequestMappingHandlerAdapter。此映射器和适配器MVC Java Config默认的映射器和适配器。
>
> 特别指出：@RestController不支持DefaultAnnotationHandlerMapping-AnnotationMethodHandlerAdapter对，两个类也被废弃



```
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documtented
@Controller
@ResponseBody
public @interface RestController{
    
    String value() default "";
}
```



