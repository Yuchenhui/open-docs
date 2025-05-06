Rate评价
======

基础用法
-------------------------------------------------------------------------------------

通过将`type`属性的值指定为`rate`

```vue
<avue-form  :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        option:{
          column: [{
              label: '评价',
              prop: 'rate',
              type: 'rate',
          }, {
              label: '评价',
              prop: 'rate',
              type: 'rate',
              colors: ['#99A9BF', '#F7BA2A', '#FF9900']
          }]
        }
      };
    }
}
</script>
```

辅助文字
-------------------------------------------------------------------------------------

> 用辅助文字直接地表达对应分数

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        option:{
          column: [{
              label: '评价',
              prop: 'rate',
              type: 'rate',
              showText: true,
              texts: ['极差', '失望', '一般', '满意', '惊喜'],
          }]
        }
      };
    }
}
</script>
```

自定义图标
-----------------------------------------------------------------------------------------------

> 当有多层评价时，可以用不同类型的 icon 区分评分层级

设置`iconClasses`属性可以自定义不同分段的图标。若传入数组，共有 3 个元素，为 3 个分段所对应的类名；若传入对象，可自定义分段，键名为分段的界限值，键值为对应的类名。本例还使用`voidIconClass`指定了未选中时的图标类名。

```vue
<avue-form :option="option" ></avue-form>

<script>
export default {
    data() {
      return {
        option:{
          column: [{
              label: '评价',
              prop: 'rate',
              type: 'rate',
              iconClasses: ['el-icon-circle-close', 'el-icon-remove', 'el-icon-circle-plus'],
              voidIconClass: "el-icon-circle-plus-outline"
          }]
        }
      };
    }
}
</script>
```

自定义个数
-----------------------------------------------------------------------------------------------

长度应等于最大值`max`。

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        option:{
          column: [{
              label: '评价',
              prop: 'rate',
              type: 'rate',
              max: 40
          }]
        }
      };
    }
}
</script>
```

只读
-----------------------------------------------------------------

> 只读的评分用来展示分数，允许出现半星

为组件设置 `disabled` 属性表示组件为只读，支持小数分值。此时若设置 `showScore`，则会在右侧显示目前的分值。可以提供 `scoreTemplate` 作为显示模板，模板为一个包含了 `{value}` 的字符串，`{value}` 会被解析为分值。

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        option:{
          column: [{
              label: '评价',
              prop: 'rate',
              type: 'rate',
              value: 3.7,
              disabled:true,
              showScore: true,
              scoreTemplate:"{value}"
          }]
        }
      };
    }
}
</script>
```

[Color颜色选择器](https://v2.avuejs.com/form/form-input-color/) [Slider滑块](https://v2.avuejs.com/form/form-slider/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号