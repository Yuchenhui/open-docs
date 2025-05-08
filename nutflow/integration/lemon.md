Lemon 集成

Lemon 插件实现方式为 Saber3 相同的 options api + js，未采用 Vue3 最新的 composition api + ts 语法。后续将持续更新过度。

TIP

* 若你购买了Lemon授权但插件私服没有Lemon项目，请访问 [https://notify.nutflow.vip/api/lemon/check/{qq}](https://notify.nutflow.vip/api/lemon/check/%7Bqq%7D)，将{qq}替换为自己的授权qq，然后到工作流插件私服获取代码。若获取失败则表示不符合工作流插件和Lemon的同时授权情况。
* 插件私服的Lemon会定期同步原Lemon私服的代码，可直接使用。
* 若不使用插件私服的Lemon，下面文档中提到的复制、拷贝均指的是插件私服的Lemon复制到你原有的Lemon项目中。

TIP

插件的菜单是`协同办公`，不是 Lemon 自带的`我的事务`和`流程管理`！！！

1、插件私服创建 token

登录插件私服 -> 右上角用户头像 -> 设置 -> 应用 -> 输入令牌名称 -> Select permissions 选择`package` `Read and Write` -> 生成令牌

![](https://cdn.nutflow.vip/docs/set_token.jpg)![](https://cdn.nutflow.vip/docs/image-20230409113151141.png)

WARNING

* token 只需要生成一次。
* 请妥善保管自己的 token，泄露可能会导致账号财产丢失。若 token 泄露，请在应用里把 token 删掉，重新生成。

2、根目录创建.npmrc 文件(可能需要点击 package.json 左侧下拉展开)

若文件存在请进行下一步  
.npmrc

```
public-hoist-pattern[]=husky
public-hoist-pattern[]=*eslint*
public-hoist-pattern[]=*prettier*
public-hoist-pattern[]=lint-staged
public-hoist-pattern[]=*stylelint*
public-hoist-pattern[]=@commitlint/cli
public-hoist-pattern[]=@vben/eslint-config

//由于vite的限制，仅可通过软件包的形式依赖
//请前往git系统创建token并配置，便可以进行依赖安装
@saber:registry=https://center.javablade.com/api/packages/blade/npm/
//center.javablade.com/api/packages/blade/npm/:_authToken=xxxxxx
```

3、.npmrc 中添加内容

```
@nutflow:registry=https://git.nutflow.vip/api/packages/blade-workflow/npm/
//git.nutflow.vip/api/packages/blade-workflow/npm/:_authToken={TOKEN}
```

把{TOKEN}替换成第 1 步生成的 token

WARNING

* @saber 开头的依赖装不上请查看 BladeX 的[文档](https://center.javablade.com/blade/BladeX-Doc/src/branch/master/%E7%AC%AC1%E7%AB%A0%20%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B/1.3%20%E5%B7%A5%E7%A8%8B%E5%AF%BC%E5%85%A5/1.3.0%20%E9%85%8D%E7%BD%AE%E8%B5%84%E6%BA%90%E4%BB%A4%E7%89%8C.md)或到 BladeX 群里询问！！！
* @saber 的 token 是 BladeX 私服的 token
* @nutflow 的 token 是插件私服的 token

4、安装依赖

sh

```
pnpm i @nutflow/nf-form-antdv @nutflow/nf-form-design-antdv @nutflow/nf-design-antdv -w
```

安装依赖可能遇到的问题

**.npmrc中@nutflow的token不正确，不用怀疑，请仔细检查。例如用了bladex的token或者带了{}。报错如下：**

* Couldn't find package "@nutflow/nf-form-xxx" on the "npm" registry.
* 401 Unauthorized - GET [https://git.nutflow.vip/api/packages/blade-workflow/npm/@nutflow%2Fnf-design-xxx](https://git.nutflow.vip/api/packages/blade-workflow/npm/@nutflow%2fnf-design-xxx)

**.npmrc未配置@nutflow的源，参考2、3步骤。或者.npmrc文件未生效，请自行百度解决。报错如下：**

* Error: [https://registry.npmmirror.com/@nutflow%2Fnf-form-xxx:](https://registry.npmmirror.com/@nutflow%2fnf-form-xxx:) Not found
* Not Found - GET [https://registry.npmjs.org/@nutflow%2Fnf-design-xxx](https://registry.npmjs.org/@nutflow%2fnf-design-xxx) - Not found

5、拷贝页面到/src/views/plugin 目录下

若 plugin 目录不存在请自行创建

![](https://cdn.nutflow.vip/docs/lemon3.jpg)

6、配置/src/main.ts

放在 `app.mount('#app')` 之前

js

```
import { registerNutflow } from "/@/views/plugin/workflow/index";

...

// 注册Nutflow
registerNutflow(app);
```

![](https://cdn.nutflow.vip/docs/lemon1.jpg)

![](https://cdn.nutflow.vip/docs/lemon2.jpg)

7、配置/src/router/routes/basic.ts

最下方添加静态路由定义

![](https://cdn.nutflow.vip/docs/lemon4.jpg)

js

```
export const WORKFLOW: AppRouteRecordRaw = {
  path: "/workflow",
  name: "workflow",
  component: LAYOUT,
  code: "workflow",
  meta: {
    title: "工作流程",
    hideBreadcrumb: true,
  },
  children: [\
    {\
      path: "design/process/:id",\
      name: "design",\
      code: "design",\
      meta: {\
        title: "模型设计2",\
        hideBreadcrumb: true,\
      },\
      component: () =>\
        import("/@/views/plugin/workflow/pages/design/index.vue"),\
    },\
    {\
      path: "design/model/history/:id",\
      name: "designModelHistory",\
      code: "designModelHistory",\
      meta: {\
        title: "模型历史",\
        hideBreadcrumb: true,\
      },\
      component: () =>\
        import("/@/views/plugin/workflow/pages/design/model-history.vue"),\
    },\
    {\
      path: "design/form/history/:id",\
      name: "designFormHistory",\
      code: "designFormHistory",\
      meta: {\
        title: "表单历史",\
        hideBreadcrumb: true,\
      },\
      component: () =>\
        import("/@/views/plugin/workflow/pages/design/form-history.vue"),\
    },\
    {\
      path: "process/start/:params",\
      name: "processStart",\
      code: "processStart",\
      meta: {\
        title: "新建流程2",\
        hideBreadcrumb: true,\
      },\
      component: () =>\
        import("/@/views/plugin/workflow/pages/process/form/start.vue"),\
    },\
    {\
      path: "process/detail/:params",\
      name: "processDetail",\
      code: "processDetail",\
      meta: {\
        title: "流程详情",\
        hideBreadcrumb: true,\
      },\
      component: () =>\
        import("/@/views/plugin/workflow/pages/process/form/detail.vue"),\
    },\
  ],
};
```

8、配置/src/store/modules/permission.ts

图片中这两处加上 WORKFLOW

![](https://cdn.nutflow.vip/docs/lemon6.jpg)

![](https://cdn.nutflow.vip/docs/lemon5.jpg)

9、配置/src/components/Button/src/BasicButton.vue

若以下代码已存在请忽略此步骤

vben 框架重写了 antdv 的 button，而插件使用了原生的 antdv button，需要修改下重写的组件以达到和原生一样的效果。

html

```
<slot name="icon"></slot>
```

![](https://cdn.nutflow.vip/docs/lemon7.jpg)

10、集成完毕后插件中使用的Modal样式错乱

因Vben项目修改了antdv的Modal全局样式，而且未做样式隔离会导致第三方使用antdv中的组件样式错乱。已提[issue](https://github.com/vbenjs/vue-vben-admin/issues/3582)，是否解决请自行关注。或者自行修改Lemon框架中的Modal组件，在组件和css中加上父级样式。