RepositoryService

主要用于对模型的部署、查询等操作。

提示

所有api都可百度查询到，或者直接询问[deepseek](https://chat.deepseek.com/)。

模型部署

```java
repositoryService.createDeployment() // 创建部署
    .name(String name) // 名称
    .key(String key) // key
    .addBpmnModel(String resourceName, BpmnModel bpmnModel) // bpmn模型对象
    .category(String category) // 分类
    .tenantId(String tenantId) // 租户
    .deploy(); // 执行部署
```

获取BpmnModel

xml中配置的信息都能用此获取到，可参考WfModelUtil。

```java
BpmnModel bpmnModel = repositoryService.getBpmnModel(String processDefId);
```

查询模型部署

```java
// 自行组合api，不认识英文找个翻译或参考常见api
repositoryService.createDeploymentQuery()
    ...
```

查询部署的模型定义

```java
// 自行组合api，不认识英文找个翻译或参考常见api
repositoryService.createProcessDefinitionQuery()
    ...
```