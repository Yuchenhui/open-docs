Skeleton 骨架屏
============

在需要等待加载内容的位置提供一个占位图。
* 网络较慢，需要长时间等待加载处理的情况下。
* 图文信息内容较多的列表/卡片中。

Tips  
1.0.7+

水平
----

最简单的占位效果。  
最后一行占满的效果  
带头像的效果  
自定义行数的效果  
自定义列表的效果  
动态切换效果

加载的内容

```html
最简单的占位效果。
<avue-skeleton></avue-skeleton>
<br />
最后一行占满的效果
<avue-skeleton block></avue-skeleton>
<br />
带头像的效果
<avue-skeleton avatar></avue-skeleton>
<br />
自定义行数的效果
<avue-skeleton avatar :rows="5"></avue-skeleton>
<br />
自定义列表的效果
<avue-skeleton avatar :rows="4" :number="3"></avue-skeleton>
<br />
动态切换效果
<el-switch :active-value="false" :inactive-value="true" v-model="loading" active-color="#13ce66"
  inactive-color="#ff4949">
</el-switch>
<avue-skeleton :loading="loading">
  <span>加载的内容</span>
</avue-skeleton>
<script>
export default {
  data(){
    return {
      loading:true,
    }
  }
}
</script>
```

Variables
---------

| 参数   | 说明           | 类型    | 可选值     | 默认值 |
| ------ | -------------- | ------- | ---------- | ------ |
| active | 是否展示动画效果 | Boolean | true/false | true   |
| avatar | 是否显示头像占位图 | String  | true/false | false  |
| loading | 是否显示骨架屏   | Boolean | true/false | true   |
| rows   | 设置段落的行数  | Number  | -          | 3      |
| block  | 最后一行是否占满 | Boolean | true/false | false  |

[Flow 流程](https://v2.avuejs.com/default/flow/) [Article 文章](https://v2.avuejs.com/default/article/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号