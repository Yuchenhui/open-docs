Rider集成

===========================================================================================

WARNING

使用前须知：Rider使用的是uni-app框架，所以兼容h5、小程序、APP等，但各平台也存在差异无法统一。移动端组件限制，某些功能也无法实现。

| 平台  | 动态组件 | 子表单 | 多选  | 字段联动 |
| --- | --- | --- | --- | --- |
| H5  | ✅   | ✅   | ❌   | ✅   |
| 小程序 | ❌   | ✅   | ❌   | ❌   |
| APP | ❌   | ✅   | ❌   | ✅   |

具体请查看wf-ui/util/unsupport.js

1、引入wf-ui

### 1.1、简介
wf-ui是工作流插件基于uView1.x封装的一套表单组件，可直接使用avue的json来渲染移动端表单组件。除部分移动端限制无法适配外，其他与PC端avue表现一致。

### 1.2、拷贝
![](https://cdn.nutflow.vip/docs/image-20220221160753013.png)

### 1.3、main.js引入(放在uView引入下面)
js
```javascript
import wfUI from "./components/wf-ui";
Vue.use(wfUI);

// #ifdef H5
// 小程序不支持动态组件
import WfCustomFields from "./pages/plugin/workflow/components/custom-fileds/index.js";
Vue.use(WfCustomFields);
// #endif
```

### 1.4、/pages.json配置eazycom
json
```json
"easycom": {
  "^u-(.*)": "@/uview-ui/components/u-$1/u-$1.vue",
  "^wf-(.*)": "@/components/wf-ui/components/wf-$1/wf-$1.vue"
},
```

2、拷贝插件至以下目录
![](https://cdn.nutflow.vip/docs/image-20220221161938784.png)

3、/pages.json中添加路由
js
```javascript
// ****************流程设计器
{
  "path": "pages/plugin/workflow/pages/workbench/index",
  "style": {
    "navigationBarTitleText": "工作台",
    "enablePullDownRefresh": true,
    "navigationStyle": "custom"
  }
},
{
  "path": "pages/plugin/workflow/pages/create/index",
  "style": {
    "navigationBarTitleText": "新建流程",
    "enablePullDownRefresh": true,
    "navigationStyle": "custom"
  }
},
{
  "path": "pages/plugin/workflow/pages/mine/index",
  "style": {
    "navigationBarTitleText": "我的事务",
    "enablePullDownRefresh": true,
    "navigationStyle": "custom"
  }
},
{
  "path": "pages/plugin/workflow/pages/form/start",
  "style": {
    "navigationBarTitleText": "发起流程",
    "enablePullDownRefresh": false
    // "navigationStyle": "custom"
  }
},
{
  "path": "pages/plugin/workflow/pages/form/detail",
  "style": {
    "navigationBarTitleText": "流程详情",
    "enablePullDownRefresh": false
    // "navigationStyle": "custom"
  }
},
{
  "path": "pages/plugin/workflow/pages/external/Leave/start",
  "style": {
    "navigationBarTitleText": "发起流程",
    "enablePullDownRefresh": false
    // "navigationStyle": "custom"
  }
},
{
  "path": "pages/plugin/workflow/pages/external/Leave/detail",
  "style": {
    "navigationBarTitleText": "流程详情",
    "enablePullDownRefresh": false
    // "navigationStyle": "custom"
  }
}
```

TIP

外置表单也需要在此手动添加路由

4、添加页面入口
在Rider的任意位置添加跳转路由 `/pages/plugin/workflow/pages/workbench/index`，由此可进入工作流插件中。如：
![](https://cdn.nutflow.vip/docs/image-20220221163920499.png)