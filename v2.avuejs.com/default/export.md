Export excel导出/导出
=================

Tips

2.0.3+

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里）-->
<script src="https://cdn.staticfile.net/FileSaver.js/2014-11-29/FileSaver.min.js"></script>
<script src="https://cdn.staticfile.net/xlsx/0.18.2/xlsx.full.min.js"></script>
```

Excel导出
---------------------------------------------------------------------------

下载 excel 下载 多级表头excel

```html
<div style="width:400px">
 <el-button type="primary" @click="handleExcel">下载 excel</el-button>
 <el-button type="success" @click="handleExcel1">下载 多级表头excel</el-button>
</div>
<script>
export default {
  data(){
    return {}
  },
  methods: {
     handleExcel() {
      let opt = {
        title: '文档标题',
        column: [{
          label: '标题',
          prop: 'title'
        }],
        data: [{
          title: "测试数据1"
        }, {
          title: "测试数据2"
        }]
      }
      this.$Export.excel({
        title: opt.title ,
        columns: opt.column,
        data: opt.data
      });
    },
    handleExcel1() {
      let opt = {
        title: '文档标题',
        column: [{
          label:'多级表头',
          prop:'header',
          children:[
            {
              label: '标题1',
              prop: 'title1'
            },{
              label: '标题2',
              prop: 'title2'
            }
          ]
        }],
        data: [{
          title1: "测试数据1",
          title2: "测试数据2"
        }, {
          title1: "测试数据2",
          title2: "测试数据2"
        }]
      }
      this.$Export.excel({
        title: opt.title,
        columns: opt.column,
        data: opt.data
      });
    }
  }
}
</script>
```

Variables
---------------------------------------------------------------

| 参数  | 说明  | 类型  | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| title | 标题  | String | -  | new Date().getTime() |
| column | 数据列 | Array | -  | -  |
| data | 数据  | Array | -  | -  |

Excel导入
---------------------------------------------------------------------------

下载模版

导入 excel

```html
<div style="display:flex;">
 <el-button type="primary" @click="handleGet" >下载模版</el-button>
 <div style="width:20px;"></div>
 <el-upload :auto-upload="false" :show-file-list="false" action="action" :on-change="handleChange">
  <el-button type="primary">导入 excel</el-button>
 </el-upload>
</div>
<br />
<avue-crud :option="option" :data="list"></avue-crud>
<script>
export default {
  data(){
    return {
      list:[],
      option:{
        column:[{
          label:'id',
          prop:'id'
        },{
          label:'姓名',
          prop:'name'
        },{
          label:'年龄',
          prop:'sex'
        }]
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
          this.list=data.results;
        })
    }
  }
}
</script>
```