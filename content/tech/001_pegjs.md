+++
date = "2017-02-05T18:14:10+08:00"
title = "DSL领域建模利器PEGjs"

+++



# DSL领域建模利器 PEG.js

开发过程中经常会为了合理分离代码的业务部分和技术部分，把问题域抽象为一种DSL领域建模表达，领域建模语言只关注业务，不会出现技术代码，故非常便于快速业务堆叠和后期业务逻辑维护。

但自己发明的DSL，需要自己配套实现一个解析引擎来转换为技术实现，之前一直用纯文本来存储和表达，但手写解析器相当麻烦且不专业（字符串拆解），后期提供了DSL的可视化设计界面，改用JSON存储，格式很规整，但牺牲了文本可编辑性，也偏离了DSL的意义；还有办法就是用YACC那些编译原理的套路实现，很正统但是上手复杂，杀鸡不值得动用牛刀。

刷微博偶遇PEG.js，把DSL解析工作简化的相当人性化，把格式语法定义出来，解析器也就完成了，真是相见恨晚。

以做个的一个工作流模块为例，之前设计的DSL格式是这样的：

> flow 事件列表
> init:
>    c.录入 info -> c.未处理
>    c.批量导出 info2 -> c.未处理
>    c.处理登记 info3 -> c.未处理
>    c.推送消息 info2 -> c.处理中
>    c.派发公文 info2 -> c.处理中
> c.未处理:
>    c.派发公文 info2 -> c.处理中
> c.处理中:
>    c.处理登记 info3 -> c.已处理

flow 声明一个工作流，后面是一堆FSM状态机，每个状态下接受多个Action，每个Action后跟着工作流状态表单以及下一个状态，解析引擎会根据这个工作流的DSL自动运转，之前徒手解析上述语法相当费事且浪费时间，代码略，改用PEG.js，只需如下语法定义，一个解析器就完成了。

```javascript
Flow = "flow" _ name:Name _ states:( State )+ {
   return {name:name, states:states};
}

State = name:Name ":" _ trans:( Trans )+ {
   return {name:name, trans:trans};
}

Trans = from:Name _ form:Name _ "->" _ to:Name _ {
   return {from:from, form:form, to:to};
}

Name = [\u4E00-\u9FA5\uf900-\ufa2da-zA-Z0-9_.]+ {
   return text();
}

_ "whitespace"
  = [ \t\n\r]*
```

PEGjs的语法相当简单，会使用正则表达式的朋友一看即懂，PEGjs支持即时插入javascript片段来自定义解析过程处理，对于表达式类型的DSL文法相当擅长。

PEGjs不直接支持左递归文法的问题，在设计DSL时回避即可，其实几乎不会用到。

### 总结

时间很宝贵，业务密集型的代码务必拆分业务部分和技术部分，请用DSL；

时间很宝贵，DSL设计完成后，解析代码切勿徒手实现，请用Parser generator，如果是Javascript技术栈，请用PEG.js。

官网链接：[pegjs.org](pegjs.org)
