# 使用HTTP实体(Using HttpEntity)
`HttpEntity`与`@RequestBody`和`@ResponseBody`很相似。除了可以访问请求和响应体，`HttpEntity`(和特舒响应子类`ResponseEntity`)也允许访问请求和响应头，像下面这样：


```
@RequestMapping("/something")
public ResponseEntity<String> handle(HttpEntity<byte[]> requestEntity) throws UnsupportedEncodingException{
    String requestHeader = requestEntity.getHeaders().getFirst("MyRequestHeader"));
    byte[] requestBody = requestEntity.getBody();
    
    HttpHeaders responseHeaders = new HttpHeaders();
    responseHeaders.set("MyResponseHeader", "MyValue");
    return new ResponseEntity<String>("Hello World", responseHeaders, HttpStatus.CREATED);
}
```
上面的示例获取了请求头中`MyRequestHeader`的值，以二进制数组的方式读取值，并把`MyRequestHeader`添加到响应头中，把`Hello World`写入响应流中，并把响应码设置为201(创建)

像`@RequestBody`和`@ResponseBody`，Spring使用`HttpMessageConverter`转换响应和请求流。关于这个转换的更详细信息，参阅前面一章和[Message Converters](/Message Converters)

