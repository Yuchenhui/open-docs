国际化
===

介绍  
Avue 采用中文作为默认语言，同时支持多语言切换，请按照下方教程进行国际化设置。

使用方法  
多语言切换

```javascript
// 完整引入 Avue
import Vue from 'vue'
import Avue from '@smallwei/avue'
import zhLocale from '@smallwei/avue/lib/locale/lang/zh'
import enLocale from '@smallwei/avue/lib/locale/lang/en'

Vue.use(Avue, { locale: enLocale })
```

语言包  
目前支持的语言:

| 语言  | 文件名 |
| --- | --- |
| 简体中文 | zh  |
| 英语  | en  |

常见问题  
Avue-cli中的引入

```javascript
//参考文件
//https://gitee.com/smallweigit/avue-cli/blob/2.x/src/lang/index.js
import zhLocale from '@smallwei/avue/lib/locale/lang/zh'
import enLocale from '@smallwei/avue/lib/locale/lang/en'
const messages = {
  en: {
    ...enLocale
  },
  zh: {
    ...zhLocale
  }
}
```

找不到所需的语言包？  
如果上方列表中没有你需要的语言，欢迎给我们提 Pull Request 来增加新的语言包。

业务代码如何实现国际化？  
可以使用 [vue-i18n (opens new window)](https://github.com/kazupon/vue-i18n) 来实现。

以 CDN 形式引入时，如何使用语言包？  
目前没有提供 CDN 形式的语言包，可以手动拷贝语言包的内容来使用。

[全局配置](https://v2.avuejs.com/docs/global/) [全局api](https://v2.avuejs.com/docs/api/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本  

关注Avue Cloud公众号