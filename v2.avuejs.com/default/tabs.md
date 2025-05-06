Tabs 选项卡
========
常用的表单和表格选项卡，可以与form他组件组合使用

普通用法
-----------------------------------------------------------------------------------
选项卡内容1

使用方法和常规用法一样`option`配置结构体，同时包含了一个`change`回调事件

```vue
<avue-tabs :option="option" @change="handleChange"></avue-tabs>
<span v-if="type.prop==='tab1'">选项卡内容1</span>
<span v-else-if="type.prop==='tab2'">选项卡内容2</span>
<span v-else-if="type.prop==='tab3'">选项卡内容3</span>
<script>
export default {
  data(){
    return {
        type:{},
        option:{
          // stretch:true,
          // beforeLeave: (active) => {
          //   console.log(active)
          // },
          // position: 'left',//left|right|top|bottom
          column: [{
            icon:'el-icon-info',
            label: '选项卡1',
            prop: 'tab1',
          }, {
            icon:'el-icon-warning',
            label: '选项卡2',
            prop: 'tab2',
          }, {
            icon:'el-icon-question',
            label: '选项卡3',
            prop: 'tab3',
          }]
        }
    }
  },
  created(){
    this.type = this.option.column[0];
  },
  methods:{
    handleChange(column) {
      this.type = column
      this.$message.success(JSON.stringify(column))
    }
  }
}
</script>
```