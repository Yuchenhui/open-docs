Object对象形式
==========

Tips

2.10.12+

之前的版本option中column是数组的格式，2.10.12+后支持对象格式，操作更加方便

`option`中的`column`可以配置成对象形式，用`prop`作为`key`

```vue
<avue-crud :option="option" :data="data" ></avue-crud>

<script>
export default {
  data () {
    return {
      form: {},
      data: [{
        name: '姓名',
        sex: 14
      }],
      option: {
        labelWidth: 120,
        column: {
          name: {
            label: '姓名',
          },
          sex: {
            label: '年龄',
          }
        }
      }
    }
  },
  created () {
    this.option.column.name.label += '(name)';
  }
}
</script>
```

[Crud属性文档](https://v2.avuejs.com/crud/crud-doc/) [分页](https://v2.avuejs.com/crud/crud-page/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号