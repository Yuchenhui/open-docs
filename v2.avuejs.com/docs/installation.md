快速上手
====

快速上手
========================================================================================

介绍

通过本章节你可以了解到 Avue 的安装方法和基本使用姿势。

安装

通过 npm 安装

在现有项目中使用 Avue 时，可以通过 npm 或 yarn 进行安装(需要先引入ElementUI作为依赖支持)：

    npm i @smallwei/avue@latest-v2 -S
    yarn add @smallwei/avue@latest-v2 -S

```js
//需要先安装ElementUI的依赖
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import Avue from '@smallwei/avue';
import '@smallwei/avue/lib/index.css';
Vue.use(ElementUI)
Vue.use(Avue);
```

使用字典需要引入axios

```js
import axios from 'axios'
Vue.use(Avue,{axios})

//老版本需要使用如下
//main.js
window.axios = axios
```

通过 CDN 安装

使用 Avue 最简单的方法是直接在 html 文件中引入 CDN 链接(引入的是最新的Avue版本，当然你也可以指定版本号)，之后你可以通过全局变量 AVUE 访问到所有组件。

```html
<!-- 引入样式文件 -->
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/@smallwei/avue/lib/index.css"
/>
<link 
  rel="stylesheet" 
  href="https://unpkg.com/element-ui/lib/theme-chalk/index.css"
/>
<!-- 引入相关JS 文件 -->
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@smallwei/avue/lib/avue.min.js"></script>

<div id="app"></div>
<script>
  // 在 #app 标签下渲染一个按钮组件
  new Vue({
    el:'app',
    data(){
      return{}
    }
  });
  app.use(AVUE);
</script>
```

你可以通过以下免费 CDN 服务来使用 Avue:

[jsdelivr (opens new window)](https://www.jsdelivr.com/package/npm/@smallwei/avue) [unpkg (opens new window)](https://unpkg.com/)

通过脚手架安装

在新项目中使用 Avue 时，推荐使用 Vue 官方提供的脚手架 Vue Cli 创建项目并安装 Avue

```bash
# 安装 Vue Cli
npm install -g @vue/cli

# 创建一个项目
vue create hello-world

# 创建完成后，可以通过命令打开图形化界面，如下图所示
vue ui

# 在图形化界面中，点击 依赖 -> 安装依赖，然后将 @smallwei/avue 添加到依赖中即可。
```

[贡献指南](https://v2.avuejs.com/docs/contribution/) [全局配置](https://v2.avuejs.com/docs/global/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号