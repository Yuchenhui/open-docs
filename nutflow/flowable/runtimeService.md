RuntimeService

主要用于查询、操作运行中数据。此处只列举群里最常问几个api，其他参考插件WfProcess服务类。

提示

所有api都可百度查询到，或者直接询问[deepseek](https://chat.deepseek.com/)。

启动流程

根据流程定义id、流程定义key等条件发起流程。

java
```java
// 启动前需指定流程发起人 - 必须
identityService.setAuthenticatedUserId(userId);
// 根据不同参数启动
runtimeService.startProcessInstanceByXXX
// 清空flowable缓存
identityService.setAuthenticatedUserId(null);
```
或使用builder自定义条件

java
```java
// 自行组合api，不认识英文找个翻译或辞职
runtimeService.createProcessInstanceBuilder()
        ...
        .start();
```

查询流程

java
```java
// 自行组合api，不认识英文找个翻译或参考常见api
runtimeService.createProcessInstanceQuery()
        ...
```

获取流程发起人

java
```java
// 上一步获取的ProcessInstance
ProcessInstance processInstance = runtimeService.createProcessInstanceQuery()
        ...
        .singleResult();

String userId = processInstance.getStartUserId();
```

查询变量

java
```java
// 自行组合api，不认识英文找个翻译或参考常见api
runtimeService.createVariableInstanceQuery()
        ...
```

获取流程变量

java
```java
// 获取实例流程中全部变量
Map<String, Object> variables = runtimeService.getVariables(String processInsId);

// 获取流程实例中某个变量
Object variable = runtimeService.getVariable(String processInsId, String variableName);
T variable = runtimeService.getVariable(String processInsId, String variableName, Class<T> variableClass);
```

改变流程变量

java
```java
// 改变某一变量
runtimeService.setVariable(String processInsId, String variableName, Object value);

// 改变某些变量，相同变量名会覆盖
runtimeService.setVariables(String processInsId, Map<String, ? extends Object> variables);
```

DANGER

RuntimeService、TaskService只能对【运行中】数据查询、操作。当流程结束后【运行中】数据会删除！此时再用这俩service会报空指针或流程不存在等异常。