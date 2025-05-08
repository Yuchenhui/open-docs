Saber Vue3集成

TIP
* Saber3项目为Vue3版本。工作流插件作为Saber3框架的一部分呈现。
* 本项目会同步BladeX私服的Saber3更新。若您的项目需要使用最新的Saber3，插件私服中的此项目可直接使用，只需注意配置前4项。
* 若不使用插件私服的Saber3，以下文档中提到的复制、拷贝均指的是插件私服的Saber3复制到你原有项目的Saber3。

TIP
插件的菜单是`协同办公`，不是BladeX自带的`我的事务`和`流程管理`！！！

1、插件私服创建token
登录插件私服 -> 右上角用户头像 -> 设置 -> 应用 -> 输入令牌名称 -> Select permissions 选择`package` `Read and Write` -> 生成令牌

WARNING
* token只需要生成一次。
* 请妥善保管自己的token，泄露可能会导致账号财产丢失。若token泄露，请在应用里把token删掉，重新生成。

2、根目录创建.npmrc文件
若文件存在请进行下一步

3、.npmrc中添加内容

```
@nutflow:registry=https://git.nutflow.vip/api/packages/blade-workflow/npm/
//git.nutflow.vip/api/packages/blade-workflow/npm/:_authToken={TOKEN}
```

把{TOKEN}替换成刚才生成的token

WARNING
* @saber开头的依赖装不上请查看BladeX的[文档](https://center.javablade.com/blade/BladeX-Doc/src/branch/master/%E7%AC%AC1%E7%AB%A0%20%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B/1.3%20%E5%B7%A5%E7%A8%8B%E5%AF%BC%E5%85%A5/1.3.0%20%E9%85%8D%E7%BD%AE%E8%B5%84%E6%BA%90%E4%BB%A4%E7%89%8C.md)或到BladeX群里询问！！！
* @saber的token是BladeX私服的token
* @nutflow的token是插件私服的token

4、安装依赖

Saber版本`大于等于`4.3使用，nf-form和nf-form-design在Saber3中已提供

yarn

```sh
yarn add @nutflow/nf-design-elp echarts
```

npm

```sh
npm i @nutflow/nf-design-elp echarts
```

Saber版本`小于等于`4.2.x使用

yarn (框架vite版本低于5使用)

```sh
yarn add @nutflow/nf-form-elp @nutflow/nf-form-design-elp @nutflow/nf-design-elp echarts
```

npm

```sh
npm i @nutflow/nf-form-elp @nutflow/nf-form-design-elp @nutflow/nf-design-elp echarts
```

或者指定版本

```sh
yarn add @nutflow/nf-form-elp@1.2 @nutflow/nf-form-design-elp@1.2 @nutflow/nf-design-elp@1.2 echarts
```

安装依赖可能遇到的问题

**.npmrc中@nutflow的token不正确，不用怀疑，请仔细检查。例如用了bladex的token或者带了{}。报错如下：**

* Couldn't find package "@nutflow/nf-form-xxx" on the "npm" registry.
* 401 Unauthorized - GET https://git.nutflow.vip/api/packages/blade-workflow/npm/@nutflow%2Fnf-design-xxx

**.npmrc未配置@nutflow的源，参考2、3步骤。或者.npmrc文件未生效，请自行百度解决。报错如下：**

* Error: https://registry.npmmirror.com/@nutflow%2Fnf-form-xxx: Not found
* Not Found - GET https://registry.npmjs.org/@nutflow%2Fnf-design-xxx - Not found

**淘宝镜像源证书过期。npm.taobao.org和registry.npm.taobao.org旧域名于2021年官方公告域名更换事件，已于2022年05月31日零时起停止服务，域名HTTPS证书于2024年1月22日正式到期，不可再用。请复制报错信息自行百度解决。报错如下：**

* npm ERR! request to registry.npm.taobao.org failed, reason: certificate has expired.

**网络问题无法连接当前镜像源(一般是npm的默认源)，请百度自行解决或更改源地址。报错如下：**

* info There appears to be trouble with your network connection. Retrying…

5、拷贝文件夹到/src/views/plugin目录下

6、配置/src/router/views/index.js

WARNING
注意层级，层级错误会导致页面嵌套显示。

```js
{
  path: '/workflow',
  component: Layout,
  children: [
    {
      path: 'design/process/:id',
      name: '模型设计2',
      component: () =>
        import(/* webpackChunkName: "views" */ '@/views/plugin/workflow/pages/design/index.vue'),
    },
    {
      path: 'design/model/history/:id',
      name: '模型历史',
      component: () =>
        import(/* webpackChunkName: "views" */ '@/views/plugin/workflow/pages/design/model-history.vue'),
    },
    {
      path: 'design/form/history/:id',
      name: '表单历史',
      component: () =>
        import(/* webpackChunkName: "views" */ '@/views/plugin/workflow/pages/design/form-history.vue'),
    },
    {
      path: 'process/start/:params',
      name: '新建流程2',
      component: () =>
        import(/* webpackChunkName: "views" */ '@/views/plugin/workflow/pages/process/form/start.vue'),
    },
    {
      path: 'process/detail/:params',
      name: '流程详情',
      component: () =>
        import(/* webpackChunkName: "views" */ '@/views/plugin/workflow/pages/process/form/detail.vue'),
    }
  ]
},
```

7、可能需要修改组件引入

Saber4.3.x及以上版本请忽略此步骤。

查看Saber3/package.json中的dependencies，若存在@saber/nf-form-design-elp和@saber/nf-form-elp依赖并已正确安装请忽略此步骤。

若你的依赖装的是@nutflow/nf-form-design-elp和@nutflow/nf-form-elp，请修改Saber3/src/views/plugin/workflow/utils/module.js中的以下两个方法的@saber为@nutflow。

```js
export function loadFormModule(app) { 
  return new Promise((resolve) => {
    const nfForm = app.component("nf-form");
    if (!nfForm) {
      app.use(NfCustomFields);

      option.text = "正在加载表单组件, 请稍等...";
      const loading = ElLoading.service(option);
      import("@nutflow/nf-form-elp") 
        .then((module) => {
          app.use(module.default, nfFormOption);
          loading.close();
          resolve();
        })
        .catch((error) => {
          loading.close();
          console.error("failed to load module:", error);
        });
    } else {
      resolve();
    }
  });
}

export function loadFormDesignModule(app) { 
  return new Promise((resolve) => {
    const nfFormDesign = app.component("nf-form-design");
    if (!nfFormDesign) {
      option.text = "正在加载表单设计器, 请稍等...";
      const loading = ElLoading.service(option);
      import("@nutflow/nf-form-design-elp") 
        .then((module) => {
          app.use(module.default);
          loading.close();
          resolve();
        })
        .catch((error) => {
          loading.close();
          console.error("failed to load module:", error);
        });
    } else {
      resolve();
    }
  });
}
```

8、表单组件 - 地图选择器（高德地图）（可选）

修改Saber3/src/views/plugin/workflow/utils/module.js

```js
// Nutflow高德地图配置
const nfFormOption = {
  amap: {
    key: '',
    secret: ''
  }
}
```

常见问题

如何发布安装自己修改源码的nf三件套

适用于自己修改了表单组件、表单设计器组件、流程设计器组件后，发布并安装自己的软件包。以下以@nutflow/nf-form-elp为例。

* 1、修改package.json中的name以及version字段。如将@nutflow/nf-form-elp修改为@somename/nf-form-elp。@somename请自行定义。
* 2、修改.npmrc，添加以下内容

```
@somename:registry=https://git.nutflow.vip/api/packages/{your_git_name}/npm/
//git.nutflow.vip/api/packages/{your_git_name}/npm/:_authToken={TOKEN}
```

其中@somename是以上第1步中定义的源统一组织名称。{your_git_name}是插件私服右上角头像 -> 设置 -> 个人信息中的用户名。{TOKEN}为上面开始配置的token。请自行修改。

* 3、打包软件包。

yarn

```sh
yarn lib
```

npm

```sh
npm run lib
```

* 4、发布软件包。发布成功后会在插件私服右上角头像 -> 个人信息 -> 软件包中显示。

```sh
npm publish
```

警告  
请不要将软件包发布到npm等公共开放源中！

* 5、安装软件包

在需要使用软件包的项目（如Saber3）中同样添加第2步中的.npmrc内容。然后在终端运行安装命令，自行修改源名称。

yarn

```sh
yarn add @somename/nf-form-elp

# 可选，删除原有依赖
yarn remove @nutflow/nf-form-elp
```

npm

```sh
npm i @somename/nf-form-elp

# 可选，删除原有依赖
npm uni @nutflow/nf-form-elp
```

* 6、引用依赖

Saber4.3.x/Saber4.2.x/Lemon

```js
// /src/views/plugin/workflow/utils/module.js文件中的
@nutflow/nf-form-elp
// 修改为
@somename/nf-form-elp
```

```js
// /src/main.js
import NfForm from "@nutflow/nf-form-elp"; // 表单组件
// 修改为
import NfForm from "@somename/nf-form-elp"; // 表单组件
```

```js
// /src/views/plugin/workflow/index.js
import NfForm from "@nutflow/nf-form-elp"; // 表单组件
// 修改为
import NfForm from "@somename/nf-form-elp"; // 表单组件
```

* 7、清除缓存

若存在安装新依赖后组件的表现和原来一样的情况，可能是未清除缓存的问题。

TIP
* vite缓存：1、停止项目。2、手动删除node_modules/.vite文件夹。3、重启项目。
* 浏览器缓存：手动清除浏览器缓存。

DANGER  
以上操作均来自npm基本知识，如有错误，请自行百度。