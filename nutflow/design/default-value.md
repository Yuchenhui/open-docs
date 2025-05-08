表单默认值

* 表单默认值的配置是为了在表单设计时在相应类型的字段上加上可选项。默认值内容支持固定值或者表达式，表达式规定使用`${}`包裹，如果需要引号包裹，请务必使用双引号！！！
* 实现逻辑就是使用eval函数解析表达式的值。所以只要是能在`src/views/plugin/workflow/mixins/ex-form.js`中取到的值，表单默认值也都可以取到。
* 若表单式中的代码无法执行，则会返回原值！插件内置了6个input字段的默认值配置，使用方法一看便知。具体实现逻辑在`src/views/plugin/workflow/mixins/default-values.js`中。
* 字段类型指的是avue配置中的type。

![](https://raw.githubusercontent.com/Yuchenhui/notes/main/pic/1746692489838.png)