流程按钮 用于配置审核节点的按钮功能，插件目前已经内置了`通过` `驳回` `打印` `转办` `委托` `终止` `加签` `指定回退` 8个按钮配置，并在流程审批过程中实现了这些功能。其中`加签`操作只有在当前节点为多实例并行时才会出现。  
![](https://raw.githubusercontent.com/Yuchenhui/notes/main/pic/1746692220905.png)  
扩展按钮功能  
1、流程按钮列表中添加按钮数据  
2、模型设计中节点重新勾选已添加的按钮  
3、在以下组件中模仿已实现的按钮实现相关功能  
* Vue2 `Saber/src/views/plugin/workflow/process/components/button.vue`  
* Vue3 `Saber3/src/views/plugin/workflow/components/nf-button/index.vue`