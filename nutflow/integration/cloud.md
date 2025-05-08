[Skip to content](https://docs.nutflow.vip/guide/integration/cloud.html#VPContent)

Return to top

Cloud版集成 [​](https://docs.nutflow.vip/guide/integration/cloud.html#cloud%E7%89%88%E9%9B%86%E6%88%90)

DANGER

[Vue2版本](https://v2.cn.vuejs.org/eol/)以及Vue2版工作流插件Saber已于2023年12月31日停止维护，Saber Vue2后台版本请使用插件1.10.0（不包含）之前的版本。

TIP

插件与BladeX自带的工作流没有任何关系。BladeX自带的FlowApplication和FlowDesignApplication无需启动。

DANGER

* BladeX`3.x`版本请使用私服blade-workflow项目的`bladex3`分支
* BladeX`4.x`版本请使用私服blade-workflow项目的`bladex4`分支。

拷贝私服中的 blade-workflow 项目源码到`blade-plugin`模块下 [​](https://docs.nutflow.vip/guide/integration/cloud.html#_1%E3%80%81%E6%8B%B7%E8%B4%9D%E7%A7%81%E6%9C%8D%E4%B8%AD%E7%9A%84-blade-workflow-%E9%A1%B9%E7%9B%AE%E6%BA%90%E7%A0%81%E5%88%B0blade-plugin%E6%A8%A1%E5%9D%97%E4%B8%8B)

![](https://cdn.nutflow.vip/docs/image-20220221134415584.png)

TIP

* 若`blade-plugin`工程不存在，请参考这次[提交](https://center.javablade.com/blade/BladeX/commit/1ae7aae638f462e9a980c40a99878ce3ad764c62)
* 若你的项目修改了包名，请修改blade-workflow中application.yaml中flowable.custom-mybatis-x-m-l-mappers中的路径。

配置nacos [​](https://docs.nutflow.vip/guide/integration/cloud.html#_2%E3%80%81%E9%85%8D%E7%BD%AEnacos)

![](https://cdn.nutflow.vip/docs/image-20220221153836892.png)![](https://cdn.nutflow.vip/docs/image-20220221154303173.png)

WARNING

新增的`blade-workflow`-dev.yaml配置的名称对应的是插件WorkflowApplication.java中的项目启动名称，若对项目前缀进行了修改，请注意修改WorkflowApplication.java中的项目启动名称。

配置xss过滤 [​](https://docs.nutflow.vip/guide/integration/cloud.html#_3%E3%80%81%E9%85%8D%E7%BD%AExss%E8%BF%87%E6%BB%A4)

nacos中的`blade.yaml`

![](https://cdn.nutflow.vip/docs/image-20220221155625378.png)

yaml

    blade:
      ...
      #xss配置
      xss:
        enabled: true
        skip-url:
          - /weixin
          - /notice/submit
          - /design/model/submit
          - /design/form/submit
          - /design/condition/submit
          - /process/startProcess
          - /process/completeTask
      ...

DANGER

xss配置是blade下的xss配置，是已经存在的。上述操作是在原有基础上添加加粗行。

配置数据库 [​](https://docs.nutflow.vip/guide/integration/cloud.html#_4%E3%80%81%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE%E5%BA%93)

* 新建bladex_workflow数据库，执行bladex_workflow.sql
* 在bladex数据库中执行bladex_menu.sql，添加前端所需要的菜单
* 在Saber/前端项目中配置相应的权限

TIP

* `doc/[vue2、vue3]/flowable`中的sql脚本是全量sql，插件更新后会同步此脚本，⚠️ 执行此脚本会清空已存在的数据。
* `doc/[vue2、vue3]/update`中的sql脚本是增量sql，每次跨版本更新都会更新此脚本。

TIP

Vue3版本中

* Saber3请执行saber3_menu.sql
* Lemon请执行lemon_menu.sql

WARNING

* 若配置了application.yaml中flowable.database-schema-update: true, flowable第一次启动的时候会自动创建ACT_和FLW_开头的表，当升级flowable版本时也会自动执行flowable的升级sql。若你的项目启动不会自动创建或升级，请检查配置。想了解原理的自行百度，不想了解的直接执行群文件中的flowable6.7.2.sql（mysql BladeX3）flowable7.0.1.sql（mysql BladeX4）。其他数据库请[在此寻找](https://github.com/flowable/flowable-engine/tree/main/distro/sql)。

![](https://cdn.nutflow.vip/docs/image-20220221155748731.png)