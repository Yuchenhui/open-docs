主要用于历史数据的查询。历史数据只能查询，无法操作。 提示 所有api都可百度查询到，或者直接询问[deepseek](https://chat.deepseek.com/)。

查询流程  
java  
```java
// 自行组合api，不认识英文找个翻译或参考常见api
historyService.createHistoricProcessInstanceQuery()
		...
```

获取流程发起人  
java  
```java
// 上一步获取的ProcessInstance
HistoricProcessInstance processInstance = historyService.createHistoricProcessInstanceQuery()
		...
		.singleResult();

String userId = processInstance.getStartUserId();
```

查询任务  
java  
```java
// 自行组合api，不认识英文找个翻译或参考常见api
historyService.createHistoricTaskInstanceQuery()
		...
```

查询变量  
java  
```java
// 自行组合api，不认识英文找个翻译或参考常见api
historyService.createHistoricVariableInstanceQuery()
		...
```