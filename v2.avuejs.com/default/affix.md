Affix 图钉
========

使用图钉，可以将内容固定在屏幕上，并且不随页面的滚动而滚动。常用于侧边菜单等，往下滑动页面体验。

Tips

1.0.4+

固定在最顶部

```vue
<avue-affix :offset-top="100">
  <el-button type="primary">固定在最顶部</el-button>
</avue-affix>
<script>
export default {
  
}
</script>
```

固定在距离顶部 50px 的位置

```vue
<avue-affix :offset-top="150">
  <el-button type="primary">固定在距离顶部 50px 的位置</el-button>
</avue-affix>
<script>
export default {
  
}
</script>
```

固定在距离顶部 100px 的位置

```vue
<avue-affix :offset-top="200" >
  <el-button type="primary">固定在距离顶部 100px 的位置</el-button>
</avue-affix>
<script>
export default {
  
}
</script>
```

固定在距离顶部 150px 的位置

```vue
<avue-affix :offset-top="250" >
  <el-button type="primary">固定在距离顶部 150px 的位置</el-button>
</avue-affix>
<script>
export default {
  
}
</script>
```

用于测试长度的

```html
<div style="height:500px"></div>
<script>
export default {
  
}
</script>
```

Variables
--------------------------------------------------------------

| 参数       | 说明                        | 类型   | 可选值 | 默认值  |
|------------|-----------------------------|--------|--------|---------|
| target     | 指定父类class或者id          | String | -      | window  |
| offset-top | 距离窗口顶部达到指定偏移量后触发 | Number | -      | 0       |

[Avatar 头像](https://v2.avuejs.com/default/avatar/) [Search 搜索](https://v2.avuejs.com/default/search/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号