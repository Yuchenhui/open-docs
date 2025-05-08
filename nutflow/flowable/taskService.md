TaskService

主要用于查询、操作运行中任务数据。此处只列举群里最常问几个api，其他参考插件WfProcess服务类。

提示  
所有api都可百度查询到，或者直接询问[deepseek](https://chat.deepseek.com/)。

查询

```java
// 自行组合api，不认识英文找个翻译或参考常见api
taskService.createTaskQuery()
		...
```

人员相关

```java
// 设置审核人，有唯一审核人后候选人/组会失效。
taskService.setAssignee(String taskId, String userId);

// 设置拥有者，主要用于转办、委托标识原任务拥有者。
taskService.setOwner(String taskId, String userId);

// 任务签收，多候选人/组时首先签收的会成为唯一审核人。详见文档【我的待办】【待签事务】
taskService.claim(String taskId, String userId);
```

完成任务

```java
taskService.complete(String taskId);
```

获取变量

```java
// 获取实例流程中全部变量
Map<String, Object> variables = taskService.getVariables(String taskId);

// 获取流程实例中某个变量
Object variable = taskService.getVariable(String taskId, String variableName);
T variable = taskService.getVariable(String taskId, String variableName, Class<T> variableClass);
```

改变变量

```java
// 改变某一变量
taskService.setVariable(String taskId, String variableName, Object value);

// 改变某些变量，相同变量名会覆盖
taskService.setVariables(String taskId, Map<String, ? extends Object> variables);
```

DANGER  
RuntimeService、TaskService只能对【运行中】数据查询、操作。当流程结束后【运行中】数据会删除！此时再用这俩service会报空指针或流程不存在等异常。