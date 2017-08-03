# 针对Post方式提交的请求如果出现乱码问题，可以每次在request解析数据时设置编码格式：

* 方式一：servlet中的设置方法

```
request.setCharacterEncoding("utf-8");
```

* 试式二：spring mvc中的设置方法
  web.xml中的方法

```xml
<filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
<filter-mapping>    
```

利用Serlvet3.0的特性，清爽的java配置方法

```java
public class MyServletConfig2 implements WebApplicationInitializer {
    @Override
    public void onStartup(ServletContext servletContext) throws ServletException {
        CharacterEncodingFilter characterEncodingFilter = new CharacterEncodingFilter();
        characterEncodingFilter.setEncoding("UTF-8");
        characterEncodingFilter.setForceEncoding(true);

        FilterRegistration.Dynamic encodingFilter = servletContext.addFilter("encodingFilter", characterEncodingFilter);
        EnumSet<DispatcherType> enumSet = EnumSet.allOf(DispatcherType.class);
        encodingFilter.addMappingForUrlPatterns(enumSet,true, "/*");

    }
}
```

## 针对get方式乱码的问题

```xml
 <Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" 
            redirectPort="8443" URIEncoding="UTF-8"/>
```



