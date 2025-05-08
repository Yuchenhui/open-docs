Boot版集成

DANGER  
Vue2版本以及Vue2版工作流插件Saber已于2023年12月31日停止维护，Saber Vue2后台版本请使用插件1.10.0（不包含）之前的版本。

TIP  
插件与BladeX自带的工作流没有任何关系。BladeX自带的flow目录可删除。

DANGER  
* BladeX`3.x`版本请使用私服blade-workflow-boot项目的`bladex3`分支  
* BladeX`4.x`版本请使用私服blade-workflow-boot项目的`bladex4`分支。

1、拷贝私服blade-workflow-boot项目源码到`org.springblade.plugin`目录下  
若目录不存在请自行创建

2、pom.xml修改flowable版本  
DANGER  
BladeX2.9.1+ 请删除以下依赖  
```xml
<dependency>
  <groupId>org.springblade</groupId>
  <artifactId>blade-starter-flowable</artifactId>
</dependency>
```
添加依赖(BladeX2.9.0及以下自带以下依赖，需要修改版本号)。  

BladeX3  
```xml
<!-- 工作流 -->
<dependency>
  <groupId>org.flowable</groupId>
  <artifactId>flowable-spring-boot-starter</artifactId>
  <version>6.7.2</version>
</dependency>
```

BladeX4  
```xml
<!-- 工作流 -->
<dependency>
  <groupId>org.flowable</groupId>
  <artifactId>flowable-spring-boot-starter</artifactId>
  <version>7.0.1</version>
</dependency>
```

WARNING  
上述操作之后BladeX自带的工作流flow文件夹中会报错，请自行解决或直接删除flow文件夹。

3、配置flowable  

application.yaml  
```yaml
#flowable配置
flowable:
  activity-font-name: \u5B8B\u4F53
  label-font-name: \u5B8B\u4F53
  annotation-font-name: \u5B8B\u4F53
  check-process-definitions: false
  database-schema-update: true # 表自动更新
  async-executor-activate: false # 关闭定时任务
  app:
    enabled: false
  cmmn:
    enabled: false
  idm:
    enabled: false
  dmn:
    enabled: false
  form:
    enabled: false
  content:
    enabled: false
  eventregistry:
    enabled: false
  custom-mybatis-x-m-l-mappers:
    - org/springblade/plugin/workflow/process/mapper/WfProcessDefinition.xml
```
TIP  
若你的项目修改了包名，请自行修改上述custom-mybatis-x-m-l-mappers中的路径。

4、配置xss过滤  

application.yaml  
```yaml
blade:
  ...
  #xss配置
  xss:
    enabled: true
    skip-url:
      - /blade-chat/weixin
      - /blade-desk/notice/submit
      - /blade-workflow/design/model/submit
      - /blade-workflow/design/form/submit
      - /blade-workflow/design/condition/submit
      - /blade-workflow/process/startProcess
      - /blade-workflow/process/completeTask
  ...
```
DANGER  
xss配置是blade下的xss配置，是已经存在的。上述操作是在原有基础上添加加粗行。

5、配置数据库  
* bladex_boot数据库中执行bladex_workflow.sql  
* bladex_boot数据库中执行bladex_menu.sql，添加前端所需要的菜单  
* 在Saber项目中配置相应的权限

TIP  
* `doc/[vue2、vue3]/flowable`中的sql脚本是全量sql，插件更新后会同步此脚本，⚠️执行此脚本会清空已存在的数据。  
* `doc/[vue2、vue3]/update`中的sql脚本是增量sql，每次跨版本更新都会更新此脚本。

TIP Vue3版本中  
* Saber3请执行saber3_menu.sql  
* Lemon请执行lemon_menu.sql

WARNING  
* 在执行脚本时有时会报外键问题，是因为执行了blade-flowable的sql，请删除ACT_和FLW_开头的所有表再执行，或者暂时关闭数据库的外键检查。  
* 若配置了application.yaml中flowable.database-schema-update: true, flowable第一次启动的时候会自动创建ACT_和FLW_开头的表，当升级flowable版本时也会自动执行flowable的升级sql。若你的项目启动不会自动创建或升级，请检查配置。想了解原理的自行百度，不想了解的直接执行群文件中的flowable6.7.2.sql（mysql BladeX3）flowable7.0.1.sql（mysql BladeX4）。其他数据库请[在此寻找](https://github.com/flowable/flowable-engine/tree/main/distro/sql)。