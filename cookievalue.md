# Mapping cookie values with the @CookieValue 注解

此注解声明：一个方法参数应被绑定一个HTTP cookie

此方法参数的类型可以声明为Cookie 或者 String 类型

让我们考虑下面的cookie从请求头中接收到

```
JSESSIONID=B9CD6887F7982D584C925C70278E6469
```

下面的代码简单的示范了怎么获取JESSIONID cookie的值

```
@RequestMapping("displayHeaderInfo.do")
public void displayHeaderInfo(@CookieValue("JESSIONID") String cookie){
}
```

类型转换自动提供如果目标方法参数的类型不是String

