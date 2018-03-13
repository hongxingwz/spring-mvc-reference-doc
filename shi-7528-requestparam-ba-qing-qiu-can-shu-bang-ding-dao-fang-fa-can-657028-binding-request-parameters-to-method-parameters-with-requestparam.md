# 使用@RequestParam把请求参数绑定到方法参数(Binding request parameters to method parameters with @RequestParam)

使用`@RequestParam`注解将请求参数绑定到你的控制器方法参数

下面的代码片断展示了怎样使用：


```
@Controller
@RequestMapping("/pets")
@SessionAttributes("pet")
public class EditPetForm{

    // ...
    
    @GetMapping
    public String setupForm(@RequestParam("petId") int petId, ModelMap model){
    Pet pet = this.clinic.loadPet(petId);
    model.addAttribute("pet", pet);
    return "petForm";
    }
    
    // ...
```
使用了此注解的参数默认被要求是必须的，你可以通过设置`@RequestParams`的`required`属性为`false`(例如，`@RequestParam(name="id", required=false)`).
类型转换会自动提供如果目标方法参数不是字符串。参阅[the section called "Method Parameters and Type Conversion"](/the section called "Method Parameters and Type Conversion").

当一个`@RequestParam`注解被用于`Map<String, String>`或`MultiValueMap<String, String`> 参数时，map会填充所有的请求参数


