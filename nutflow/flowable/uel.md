Flowable 使用统一表达式语言(UEL, Unified Expression Language)来实现流程中的动态行为。可用于`条件判断` `跳过表达式` `人员配置`等。表达式使用`${}`或`#{}`包裹。* 条件、跳过表达式需要表达式的返回值为`Boolean`类型。* 人员配置支持的返回值为 `id1,id2,id3,...` 或 `[WfUser1, WfUser2, WfUser3, ...]` 或 `String [id1, id2, id3, ...]` 或 `Long [id1, id2, id3, ...]`。

提示 flowable的基本知识都可百度查询到，或者直接询问[deepseek](https://chat.deepseek.com/)。

变量表达式 假设填写的表单中有days等变量，或者使用runtimeService、taskService.setVariable设置的变量。

```java
${days > 10}                   // 大于
${days == 10}                  // 等于
${!isValid}                    // 非运算
${isValid && (days > 10)}      // 与
${isValid || isAdmin}          // 或
```

方法表达式 表达式后端代码

```java
${wfCustomUserHandler.userList(execution)} // spring bean

${wfCustomUserHandler.condition(execution, '对')} // spring bean
```

```java
@Component("wfCustomUserHandler")
@RequiredArgsConstructor
public class WfCustomUserHandler {

	public List<WfUser> userList(DelegateExecution execution, String... customParam) {
		return Arrays.asList(WfUserCache.getUser(1L), WfUserCache.getUser(2L));
	}

	public List<String> strList(DelegateExecution execution, String... customParam) {
		return Arrays.asList("1", "2");
	}

	public List<Long> longList(DelegateExecution execution, String... customParam) {
		return Arrays.asList(1L, 2L);
	}

	public String str(DelegateExecution execution, String... customParam) {
		return "1,2";
	}

	public Boolean condition(DelegateExecution execution, String... customParam) {
		String param = customParam[0];
		return "对".equals(param);
	}
}
```