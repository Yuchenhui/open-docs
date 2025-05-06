Avatar 头像
=========

用来代表用户或事物，支持图片、图标或字符展示。

Tips

1.0.7+

形状
----

头像有三种尺寸，两种形状可选。

```html
<div class="avue-line">
  <avue-avatar :size="64" icon="el-icon-circle-plus-outline"></avue-avatar>
  <avue-avatar size="large" icon="el-icon-circle-plus-outline"></avue-avatar>
  <avue-avatar icon="el-icon-circle-plus-outline"></avue-avatar>
  <avue-avatar size="small" icon="el-icon-circle-plus-outline"></avue-avatar>
</div>
<br />
<div class="avue-line">
  <avue-avatar shape="square" :size="64" icon="el-icon-circle-plus-outline"></avue-avatar>
  <avue-avatar shape="square" size="large" icon="el-icon-circle-plus-outline"></avue-avatar>
  <avue-avatar shape="square" icon="el-icon-circle-plus-outline"></avue-avatar>
  <avue-avatar shape="square" size="small" icon="el-icon-circle-plus-outline"></avue-avatar>
</div>
```

类型
----

支持三种类型：图片、Icon 以及字符，其中 Icon 和字符型可以自定义图标颜色及背景色。

```html
<div class="avue-line">
  <avue-avatar icon="el-icon-circle-plus-outline"></avue-avatar>
  <avue-avatar>U</avue-avatar>
  <avue-avatar>USER</avue-avatar>
  <avue-avatar src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png"></avue-avatar>
  <avue-avatar style="color: #f56a00; background-color: #fde3cf">U</avue-avatar>
  <avue-avatar style="background-color:#87d068" icon="el-icon-circle-plus-outline"></avue-avatar>
</div>
```

动态
----

对于字符型的头像，当字符串较长时，字体大小可以根据头像宽度自动调整。

```html
<div class="avue-line">
  <avue-avatar shape="square" size="large" :style="{backgroundColor: color, verticalAlign: 'middle'}">
    {{avatarValue}}</avue-avatar>
  <el-button size="small" style="margin-left:16px;vertical-align: 'middle'" @click="changeValue">改变</el-button>
</div>
<script>
var UserList = ['U', 'Lucy', 'Tom', 'Edward']
var colorList = ['#f56a00', '#7265e6', '#ffbf00', '#00a2ae']
export default {
  data() {
    return {
      avatarValue: UserList[0],
      color: colorList[0],
    }
  },
  methods: {
    changeValue() {
      var index = UserList.indexOf(this.avatarValue)
      this.avatarValue = index < UserList.length - 1 ? UserList[index + 1] : UserList[0]
      this.color = index < colorList.length - 1 ? colorList[index + 1] : colorList[0]
    },
  }
}
</script>
```

Variables
---------

| 参数  | 说明             | 类型   | 可选值         | 默认值  |
|-------|------------------|--------|----------------|---------|
| icon  | 设置头像的图标类型 | String | -              | -       |
| shape | 指定头像的形状    | String | circle/square  | circle  |
| size  | 设置头像的大小    | String | large/small    | -       |
| src   | 图片类头像的资源地址 | String | -              | -       |

[TextEllipsis 超出文本省略](https://v2.avuejs.com/default/text-ellipsis/) [Affix 图钉](https://v2.avuejs.com/default/affix/)