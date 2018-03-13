# 使用@RestController注解创建REST控制器(Creating REST Controllers with the @RestController annotation)

使用控制器来实现REST API是一个很常见的用例，提供JSON，XML和自定义的媒体内容。为了更方便，而不是在你的每一个@RequestMapping方法上标注@ResponseBody,你可以把你的控制器标注为@RestController。

`@RestController`是`@ResponseBody`和`@Controller`了结合起来的骨架注解。更多的是，这个注解赋予你的控制器更多的含义也可能在将来框架的版本中带来更多的语义。

像常规的`@Controller`一样，`@RestController`可以由`@ControllerAdvice`或`@RestControllerAdvice`帮助。参阅"Advising controllers with @ControllerAdvie and @RestControllerAdvice"节获取更多的信息。
