Search 搜索
=========

Tips

常用的表格或则列表的搜索组件，可以与form和crud等其他组件组合使用

普通用法
-------------------------------------------------------------------------------------

使用方法和常规用法一样`option`配置结构体，`v-model`为双向数据绑定，同时包含了一个`change`回调事件

```vue
<avue-search :option="option" v-model="form" @change="handleChange">
  <template slot="zdy" slot-scope="scope">
    <el-tag>自定义</el-tag>
  </template>
</avue-search>
<script>
export default {
  data(){
    return {
      form:{
        zt: ["370000", "620000", "610000", "110000", "410000"],
        checkbox: 0,
        jtgj: [0, 1, 2, 3, 4]
      },
      option:{
        column: [{
          label: '自定义',
          prop: 'zdy',
          slot: true
        },{
          label: '地区',
          prop: 'zt',
          dicUrl: 'https://cli.avuejs.com/api/area/getProvince',
          props: {
            label: 'name',
            value: 'code'
          }
        }, {
          label: '多选',
          prop: 'checkbox',
          multiple: false,
          dicData: [{
            label: '单层',
            value: 0
          }, {
            label: '多层',
            value: 1
          }]
        }, {
          label: '交通工具',
          prop: 'jtgj',
          dicData: [{
            label: '飞机',
            value: 0
          }, {
            label: '动车',
            value: 1
          }, {
            label: '驾车',
            value: 2
          }, {
            label: '其他',
            value: 3
          }]
        }]
      }
    }
  },
  methods:{
    handleChange(form) {
      this.$message.success(JSON.stringify(form))
    }
  }
}
</script>
```
Events
---------------------------------------------------------

| 事件名 | 说明  | 参数  |
| --- | --- | --- |
| change | 当搜索的值发生改变时的回调 | form |

[Affix 图钉](https://v2.avuejs.com/default/affix/) [Tabs 选项卡](https://v2.avuejs.com/default/tabs/)

Install Cancel

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号