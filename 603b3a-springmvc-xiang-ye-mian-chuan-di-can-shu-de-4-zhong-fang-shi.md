* 使用HttpServletRequst 和 Session 然后 setAttribute\(\)，就和Servlet中一样

```java
request.setAttribute("name", "name");
request.getSession.setAttribute("love", "dengyi");
```

* 使用ModelAndView对象

```java
@RequestMapping("/get.f")
public ModelAndView getF(){
    ModelAndView modelAndView = new ModelAndView();
    modelAndView.addObject("name", "jianglei");
    modelAndView.addObject("age", "18");
    modelAndView.addObject("love", "dengyi");
    
    modelAndView.setViewName("model/getf");
}
```

* 使用ModelMap对象

```java
@RequestMapping("/get.g")
public String getG(ModelMap map){
    map.addAttribute("name", "jianglei");
    map.addAttribute("age", "18");
    map.addAttribute("love", "dengyi");
    
    return "model/getg";
}
```

* 使用@ModelAttribute注解

```java
@RequestMapping("/get.h")
public String getH(@ModelAttribute("love") String love){
    return "model/geth";
}
```

调用时

/get.h?love=dengyi

