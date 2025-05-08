问题集锦

内置表单/外置表单/节点独立表单

内置表单

通过表单设计器设计的表单。在流程流转过程中唯一。

* 模型设计第一步设计表单。选择内置表单。
* 第二步设计流程。点击需要设计的节点，点击右侧表单配置。配置可读可写等选项。

外置表单

因复杂的表单逻辑表单设计器无法实现，用户可选择自己书写表单页面。模型设计时可配置节点的路由来达到处理节点时跳转自己页面的效果，插件会自动带入流程信息，根据流程信息自行处理相关业务。插件也内置了一个例子和一个模版，可作为参考。

通俗点的解释就是插件只负责节点跳转到你配置的页面上，并把流程信息带给你，其他不管。随便你用不用，想干什么操作在你自己的页面里干就行。

* 模型设计第一步设计表单。1、选择外置表单。2、填写表单key，用于匹配固定路径的路由。3、表单预览中填写字段和属性，对应你页面上的字段和属性，用于控制可读可写。具体可查看自带的 `请假流程 - 外置表单` 模型
* 第二步设计流程。1、点击需要设计的节点。2、点击右侧表单配置。3、表单key是第一步填写的，指向会有具体说明。4、表单路由是自己填写路由，填写后表单key的路由失效，指向也有说明，不清楚路由是什么的自行百度vue-router。5、配置可读可写等选项。

节点独立表单

特殊情况下，每个节点需要展示的表单不一样。节点上的表单可独立配置，并且还可配置汇总，会将当前节点之前的表单进行汇总。

* 模型设计第一步设计表单。选择节点独立表单。
* 第二步设计流程。1、点击需要设计的节点。2、点击右侧表单配置。3、选择表单后配置可读可写等选项。

人员配置

自定义的人员配置在哪实现

`org.springblade.plugin.workflow.process.service.impl.getTaskUser`  
节点到达时的人员、多实例节点的人员、节点未到达时可能存在的人员，都会调用此唯一的方法。

直接调用 service

消息/业务预留口

流程流转时的每一步都会自动调用此方法，如需发送消息或将流程存到自己的业务表中，可在此自行封装一个方法统一进行调用。 `org.springblade.plugin.workflow.process.service.impl.WfNoticeServiceImpl`，可通过 WfNotice.Type 区分流程的生命周期

已部署的流程，修改表单后新加的字段不显示

因表单与模型不是实时关联，所以修改表单后，模型设计中的每个节点上的 xml 表单属性还是原来的，不会随表单的改变而改变

修改表单字段prop或添加删除字段后 需打开模型设计，下一步 -> 下一步 -> 保存，即可自动刷新节点 xml。保存后重新部署即可。

flowable 监听器配置

* 事件：自行选择生命周期
* 类型：代理表达式
* 值：可自行替换成自己的 spring bean

任务监听

实现`org.flowable.engine.delegate.TaskListener`

执行监听

实现`org.flowable.engine.delegate.ExecutionListener`

监听器中获取驳回/终止等业务状态

flowable 的任务只有完成与未完成，所有驳回/终止/撤销/撤回等业务状态是插件的扩展。 在监听器中查询以下变量

```java
Object status = runtimeService.getVariable(delegateTask.getProcessInstanceId(), WfProcessConstant.TASK_VARIABLE_PROCESS_TERMINATE);
if (status != null) {
  ...
}
```

驳回

在驳回到的节点添加任务监听，且 status 为 reject

终止

在结束节点添加执行监听，且 status 为 true。 为 null 时表示正常结束。

多实例配置

正常情况下一个节点只允许一个人审批，多实例指的是一个节点可多人同时审批，目前存在串行和并行两种方式。

串行

多人按顺序依次审批。一人驳回节点驳回。

并行

多人同时审批。一人驳回节点驳回。

完成条件

假设某节点配置了 10 个人，完成条件 50%。表示 10 个人中 5 人审批通过后，此节点就会通过。

表单设计字段联动

字段联动表示表单中一个字段的值改变在业务上需要另一个字段的值也改变，或者一个字段改变需要另一字段显隐的效果。除了 avue 原生支持的 select 之间的联动外，表单设计器还支持通过事件来实现字段之间的联动。

* 改变值的操作本质是操作 form 字段中的属性，来达到改变另一字段值的效果。
* 改变字段显隐等操作的本质是操作 option 字段中的display属性，来达到改变字段属性的效果。
* 除了值改变外，基本上所有操作都是对 表单组件 的 option 的改变。

表单设计添加业务字段

* 此操作的前提是会书写 vue 组件，并了解 v-model 的原理。
* 表单设计器及表单组件中中可以渲染任何在 vue 实例中注册过的组件。这使得在表单设计器添加业务字段简单了很多。原理就是 vue 的原生组件 `<component :is="xxx">`，不了解的请自行查看 vue 文档。
* Vue3版本的配置更丰富，可参考链接

1、在`src/views/plugin/workflow/components`中编写自己的业务组件

1.1、组件的属性

1.2、当组件内值发生变化时，将改变的值映射出去

2、在`src/views/plugin/workflow/mixins/custom-fields.js`中添加自己的业务组件，添加后可在表单设计器中显示

表单设计使用事件后表单消失

同未配置 xss 拦截，导致箭头函数 => 被转义，解决办法只有把数据库中的数据复制出来，把转义的字符修改后再复制回去。

表单设计中富文本不显示

Saber 引用组件 BUG，修改如下：

Http 服务

节点调用外部 api，并且将返回的结果存到流程变量中。

Mail 服务

使用之前请先修改 application.yaml 的 flowable 配置，来配置邮件服务器

Shell 服务/脚本任务

因这两项配置对于程序来说过于危险，所以默认是不可配置的。

若了解了危险之后，可在此处打开

调用活动任务

如需在流程到达某个节点时调用另一个流程，可使用此任务。

上述任务和服务均指的是

反复点击 tag 导致路由重复的问题 Saber2

store 文件夹中 tags.js 引入 deepClone 方法

修改此文件中的 ADD_TAG 方法

```js
ADD_TAG: (state, action) => {
  state.tag = action;
  setStore({name: 'tag', content: state.tag});

  // 去除对象中的label，防止修改了tag的label后重复添加
  const tagList = deepClone(state.tagList);
  tagList.forEach(t => delete t.label);
  const tag = deepClone(action);
  delete tag.label;
  if (tagList.some(ele => diff(ele, tag))) return;

  state.tagList.push(action);
  setFistTag(state.tagList);
  setStore({name: 'tagList', content: state.tagList});
},
```

模型保存时报错

错误

* Error reading XML
* 或
* 请查看文档配置 xss 拦截

原因：未配置 xss 拦截。 boot 配置 cloud 配置

模型部署时报错

错误

Cannot resolve the name 'extension' to a(n) 'element declaration' component

原因：项目目录存在中文。

待办/待签任务区别

* 待签：正常配置的一个任务只能一个人审批，若配置多个人，则所有人都是候选人，所有候选人都可以看到这条任务。候选人需要先签收任务，这时任务的审核人会变成自己，其他人将无法看到此任务。
* 插件中待办任务包含了待签任务。

IUserSearchService/IUserSearchClient

BUG: 目前这两个类中的查询未添加租户，请自行解决或等待 BladeX 修复

boot -> IUserSearchService  
cloud -> IUserSearchClient

Rider 登录提示用户名或密码错误

* blade_client 中添加 rider 的客户端标识，直接数据库中复制添加一条即可。
* 用户名密码真的错误...