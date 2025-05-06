select选择框
=========

值:  

值:[ 0, 1 ]

```vue
<el-row :span="24">
  <el-col :span="6">
     值:{{form}}<br/>
     <avue-select v-model="form" placeholder="请选择内容" type="tree" :dic="dic"></avue-select>
  </el-col>
   <el-col :span="24"></el-col>
   <el-col :span="6">
     值:{{form1}}<br/>
     <avue-select all multiple v-model="form1" placeholder="请选择内容" type="tree" :dic="dic"></avue-select>
  </el-col>
</el-row>
<script>
export default {
    data() {
      return {
        form:'',
        form1:[0,1],
        dic:[{
          label:'选项1',
          desc:'描述1',
          disabled:true,
          value:0
        },{
          label:'选项2',
          desc:'描述2',
          value:1
        }]
      }
    }
}
</script>
```

[url超链接输入框](https://v2.avuejs.com/component/url/) [radio单选](https://v2.avuejs.com/component/radio/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
查看 Vue 3.x 的升级版本

关注Avue Cloud公众号