Saber Vue2集成

DANGER  
[Vue2版本](https://v2.cn.vuejs.org/eol/)以及Vue2版工作流插件Saber已于2023年12月31日停止维护，后台版本请使用插件1.10.0（不包含）之前的版本。

TIP  
* 本项目会同步BladeX私服的Saber更新（截止2023年12月31日）。若您的项目需要使用最新的Saber，插件私服中的此项目可直接使用，无需配置。  
* 若不使用插件私服的Saber，以下文档中提到的拷贝均指的是插件私服的Saber复制到BladeX私服的Saber。

TIP  
插件的菜单是`协同办公`，不是BladeX自带的`我的事务`和`流程管理`！！！

1、引入流程设计器与表单设计器

1.1、拷贝流程设计器与表单设计器  

![流程设计器与表单设计器](https://raw.githubusercontent.com/Yuchenhui/notes/main/pic/1746692959843.png)

1.2、配置/public/index.html  

注意这俩js的位置，是在body里面，而不是head里面！

```html
<script
	src="<%= BASE_URL %>cdn/avue-form-design/index.umd.min.js"
	charset="utf-8"
></script>
<script
	src="<%= BASE_URL %>cdn/wf-design/index.umd.min.js"
	charset="utf-8"
></script>
```

1.3、配置/src/main.js

```js
Vue.use(window.AvueFormDesign); // 表单设计器
Vue.use(window.WfDesign.default); // 流程设计器

// v1.2.5+
import WfCustomFields from "./views/plugin/workflow/components";
Vue.use(WfCustomFields); // 表单设计器业务组件
```

1.4、添加echarts依赖  

yarn

```sh
yarn add echarts
```

npm

```sh
npm i echarts
```

2、拷贝页面到/src/views/plugin目录下  

![拷贝页面](https://raw.githubusercontent.com/Yuchenhui/notes/main/pic/1746692980494.png)

3、拷贝api到/src/api/plugin目录下  

![拷贝api](https://raw.githubusercontent.com/Yuchenhui/notes/main/pic/1746693002715.png)

4、配置/src/router/views/index.js

![配置路由](https://raw.githubusercontent.com/Yuchenhui/notes/main/pic/1746693023491.png)

```js
{
  path: '/workflow',
  component: Layout,
  children: [
    {
      path: 'design/process/:id',
      name: '流程设计',
      component: () =>
        import( /* webpackChunkName: "views" */ '@/views/plugin/workflow/design'),
    },
    {
      path: 'design/model/history/:id',
      name: '模型历史',
      component: () =>
        import( /* webpackChunkName: "views" */ '@/views/plugin/workflow/design/model-history'),
    },
    {
      path: 'design/form/history/:id',
      name: '表单历史',
      component: () =>
        import( /* webpackChunkName: "views" */ '@/views/plugin/workflow/design/form-history'),
    },
    {
      path: 'process/start/:params',
      name: '新建流程',
      component: () =>
        import( /* webpackChunkName: "views" */ '@/views/plugin/workflow/process/components/form'),
    },
    {
      path: 'process/detail/:params',
      name: '流程详情',
      component: () =>
        import( /* webpackChunkName: "views" */ '@/views/plugin/workflow/process/components/detail'),
    }
  ]
}
```

5、流程设计器国际化（可选）

5.1、修改/src/main.js的引入

```js
Vue.use(window.AvueFormDesign) // 表单设计器
Vue.use(window.WfDesign.default, {
  i18n: (key, value) => i18n.t(key, value)
}) // 流程设计器

// v1.2.5+
import WfCustomFields from './views/plugin/workflow/components'
Vue.use(WfCustomFields) // 表单设计器业务组件
```

5.2、配置语言文件/src/lang/index.js

```js
import Vue from 'vue'
import VueI18n from 'vue-i18n'
import elementEnLocale from 'element-ui/lib/locale/lang/en' // element-ui lang
import elementZhLocale from 'element-ui/lib/locale/lang/zh-CN'// element-ui lang
import enLocale from './en'
import zhLocale from './zh'
import { getStore } from '@/util/store'
Vue.use(VueI18n)
const Avue = window.AVUE;
const WfDesign = window.WfDesign.default;

const messages = {
  en: {
    ...enLocale,
    ...elementEnLocale,
    ...Avue.locale.en,
    ...WfDesign.locale.en,
  },
  zh: {
    ...zhLocale,
    ...elementZhLocale,
    ...Avue.locale.zh,
    ...WfDesign.locale.zh,
  }
}

const i18n = new VueI18n({
  locale: getStore({ name: 'language' }) || 'zh',
  messages
})

export default i18n
```

6、自行配置BladeX的菜单权限