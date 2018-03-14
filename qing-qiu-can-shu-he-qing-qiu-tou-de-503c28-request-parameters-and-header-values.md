# 请求参数和请求头的值(Request Parameters and Header Values)

你可以通过请求参数条件例如"myParam", "!myParam"或者"myParam=myValue"来缩下请求匹配的范围。前两个用于验证请求参数出没出现，第三个参数用于指定参数的值。下面是用于请求参数条件的示例：


```
@Controller
@RequestMapping("/owners/{ownerId}")
public class RelativePathUriTemplateController {

    @GetMapping(path = "/pets/{petId}", params = "myParam=myValue")
    public void findPet(@PathVariable String ownerId, @PathVariable String petId, Model model) {
        // implementation omitted
    }

}
```

同样的用法可以用于检测请求头的在场和缺失，匹配基于指定请求头的值：


```
@Controller
@RequestMapping("/owners/{ownerId}")
public class RelativePathUriTemplateController {

    @GetMapping(path = "/pets", headers = "myHeader=myValue")
    public void findPet(@PathVariable String ownerId, @PathVariable String petId, Model model) {
        // implementation omitted
    }

}
```

> 尽管你可以使用媒体类型通配符匹配 Conent-Type和Accept(例如"content-type=text/*"将会匹配"text/plain" 和 "text/html"),但是推荐使用consumes 和 produces 条件来各自表示。他们就是为此目的设计的



