# Mapping request header attibute with the @RequestHeader annotation 

@RequestHeader注解允许一个方法参数绑定一个请求头参数

下面是一个简单的请求头

```
GET /jianglei/get.e HTTP/1.1
Host: localhost:8082
Connection: keep-alive
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.8,en;q=0.6
Cookie: Idea-bb3125a4=ab226eb4-4931-46c0-8946-0ed3b9ac8917; Hm_lvt_030f908df5513cb0a704c88c5da2bc37=1500943693,1501640745; Hm_lpvt_030f908df5513cb0a704c88c5da2bc37=1501641277; JSESSIONID=B9CD6887F7982D584C925C70278E6469
```

下面的代表简单的适范了怎么获得请求头Accept-Encoding和Keep-Alive的值

```java
@RequestMapping("/displayHeaderInfo.do")
public void displayHeaderInfo(@RequestHeader("Accept-Encoding") String encoding,
                                @RequestHeader("Keep-Alive") long keepAlive){
}
```

* 类型转换会自动发生如果方法的参数不是字符串类型



* 如果一个@RequestHeader注解用在了Map&lt;String, String&gt;, MultiValueMap&lt;String, String&gt; 或 HttpHeaders 参数上，此map会被填充所有的请求头

* @RequestHeader\("Accept"\) 可以是 String类型， 但也要以是String\[\] 或 List&lt;String&gt;类型



* required属性 指定的请求头是否是必要的，默认是true，如果请求头中没有指定的参数，将会抛出一个异常。将此值设置为false，如果请求头中缺少指定的参数，如该值为null



* defaultValue 默认值，如果设置了此属性，会隐式的将required设置为false



