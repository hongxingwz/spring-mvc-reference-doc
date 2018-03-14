# Controller返回String类型中文乱码问题

**例子1**


```
@RequestMapping(value = "/dd")
@ResponseBody
public String dd() {
    return "中国";
}
```

原因
* 返回的是字符串类型，spring-mvc的消息置换器没有介入
* 导致返回的响应头如下


```
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Content-Type: text/html;charset=ISO-8859-1
Content-Length: 2
Date: Wed, 14 Mar 2018 00:53:20 GMT
```
"中国"是用utf-8编码的，而响应头`Content-Type: text/html;charset=ISO-8859-1`导致浏览器解码错误

**例子2**


```
@RequestMapping(value = "/d", produces = "text/html;charset=utf-8")
@ResponseBody
public String d() {
    return "中国";
}

@RequestMapping(value = "/d2", produces = MediaType.APPLICATION_JSON_UTF8_VALUE)
@ResponseBody
public String d2() {
    return "中国";
}
```
会正确的设置`Content-Type`的编码为`utf-8`,所以浏览器解析的时候就不会乱码了。



**例子3**


```
@RequestMapping(value = "/ddd")
@ResponseBody
public List<String> ddd() {
    List<String> stringList = new ArrayList<>();
    stringList.add("中国");
    stringList.add("姜磊");

    return stringList;
}
```
在访问页面时报如下异常


```
java.lang.IllegalArgumentException: No converter found for return value of type: class java.util.ArrayList
```
没有找到`java.util.ArrayList`返回类型对应的转换器

**解决办法**
在pom.xml中添加依赖


```
<properties>
      <jackson.version>2.5.4</jackson.version>
</properties>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-core</artifactId>
  <version>${jackson.version}</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>${jackson.version}</version>
</dependency>
```










