# 方法参数和类型转换(Method Parameters And Type Conversion)

从请求中提取的基于字符串的值，包括请求参数，路径变量，请求头和cookie值都可能需要转换成目录方法参数或字段(如 使用@ModelAttribute参数绑定一个请求参数到一个字段)的类型。如果目标类型不是字符串，Spring会自动的把其转换为相应的类型。所有简单的类型例如int, long, Date 等都支持自动转换。你可以自定义转换程序通过`WebDataBinder`(参阅[the section called "Customizing WebDataBinder initialization](/the section called "Customizing WebDataBinder initialization"))或者通过`FormattingConversionService`(参阅 [Section 9.6, "Spring Field Formatting](/Section 9.6, "Spring Field Formatting"))注册`Formatters`