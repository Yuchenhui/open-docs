导入导出
====

<!-- 导入需要的包 （一定要放到index.html中的head标签里）-->
<script src="https://cdn.staticfile.net/FileSaver.js/2014-11-29/FileSaver.min.js"></script>
<script src="https://cdn.staticfile.net/xlsx/0.18.2/xlsx.full.min.js"></script>

表格导出
---------------------------------------------------------------------------------------

`excelBtn`设置为`true`即可开启导出功能

```vue
<avue-crud :option="option" :data="data"></avue-crud>
<script>
export default {
  data(){
    return {
       data:[
         {
          text1:'内容1-1',
          text2:'内容1-2',
          deep:{
             text3:'内容1-3',
          }
         },{
          text1:'内容2-1',
          text2:'内容2-2',
          deep:{
             text3:'内容2-3',
          }
         }
       ],
       option:{
          excelBtn:true,
          column: [
            {
              label: '列内容1',
              prop: 'text1',
            }, {
              label: '列内容2',
              prop: 'text2',
            }, {
              label: '列内容3',
              prop: 'text3',
              bind:'deep.text3'
            }
          ]
       }
    }
  }
}
</script>
```

表格导入
---------------------------------------------------------------------------------------

下载模版   导入 excel

```vue
<div style="display:flex;">
  <el-button size="small" type="primary" @click="handleGet" >下载模版</el-button>
  &nbsp;&nbsp;
  <el-upload :auto-upload="false" :show-file-list="false" action="action" :on-change="handleChange">
    <el-button  size="small" type="primary">导入 excel</el-button>
  </el-upload>
</div>
<br />
<avue-crud :option="option" :data="data"></avue-crud>
<script>
export default {
  data(){
    return {
      data:[],
      option:{
        column:[
          {
            label:'id',
            prop:'id'
          },{
            label:'姓名',
            prop:'name'
          },{
            label:'年龄',
            prop:'sex'
          }
        ]
      }
    }
  },
  methods: {
    handleGet(){
      window.open('/cdn/demo.xlsx')
    },
    handleChange(file, fileLis) {
      this.$Export.xlsx(file.raw)
        .then(data => {
          this.data=data.results;
        })
    }
  }
}
</script>
```