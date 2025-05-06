父子表
===

Tips

由于有的表格包含了父子表，在父表填写的完后还要填写子表的内容，由于业务场景复发多元化，如果采用配置的方法去开发，将会边不可维护，所以这里采用一种灵活的方法去实现

如下用法可以根据场景灵活使用，你可以将`infoForm`自定义内容封装成一个组件使用,这样子将会达到很好的维护效果

```vue
<avue-crud :option="option" :data="data"  v-model="form">
  <template slot="infoForm" slot-scope="scope">
     <avue-crud :option="infoOption" :data="form.info">
     </avue-crud>
  </template>
</avue-crud>
<script>
export default {
  data(){
    return {
       form:{},
       data:[{
          name:'张三',
          info:[
            {
              sex:15,
            }, {
              sex:16,
            }
          ]
       }],
       option:{
          column: [{
            label: '姓名',
            prop: 'name',
          },{
            labelWidth:0,
            label: '',
            prop: 'info',
            span:24,
            hide:true,
            formslot:true,
          }]
       },
       infoOption:{
          column: [{
            label: '年龄',
            prop: 'sex',
          }]
       }
    }
  }
}
</script>
```

[表格树](https://v2.avuejs.com/crud/crud-tree/) [行编辑](https://v2.avuejs.com/crud/crud-cell/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)  
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号