# 请求参数与请求头的值

你可以筛选请求参数的条件来缩小请求匹配范围，比如“myParam"， ”!myParam" 及 “myParam=myValue”等。前两个条件用于筛选存在/不存在某些请求参数的请求，第三个条件筛选具有特定参数值的请求。下面有个例子，展示了如何使用请求参数值的筛选条件：

```
@Controller
@RequestMapping("/owners/{ownerId}")
public class RelativePathUriTemplateController{
    
    @RequestMapping(path="/pets/{petId}", params="myParam=myValue")
    public void findPet(){
        ...
    }
}
```

同样，你可以用相同的条件来筛选请求头的出现与否，或者筛选出一个有有特定值的请求头：

```
@Controller
@RequestMapping("/owners/{ownerId}")
public class RelativePathUriTemplateController{
    @Request(path="/pets", headers="myHeader=myHeader")
    public void findPet(){
        ...
    }
}
```

> 尽管，你可以使用媒体类型的通配符\(比如“content-type=text/\*"\)来匹配请求头Content-Type和Accept的值，但我们更推荐独立使用consumers和products条件来筛选各自的请求。因为它们就是专门为区分这两种不同的场景而生的。



