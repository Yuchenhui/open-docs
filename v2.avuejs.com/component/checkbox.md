checkbox多选
==========

值:[ 0, 1 ]  
值:[]

<el-row :span="24">
  <el-col :span="6">
     值:{{form}}<br/>
    <avue-checkbox v-model="form" placeholder="请选择内容" :dic="dic"></avue-checkbox>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
     值:{{form1}}<br/>
    <avue-checkbox all v-model="form1" placeholder="请选择内容" :dic="dic"></avue-checkbox>
  </el-col>
</el-row>
<script>
export default {
    data() {
      return {
        form:[0,1],
        form1:[],
        dic:[
          {
            label:'选项1',
            value:0
          },
          {
            label:'选项2',
            value:1
          }
        ]
      }
    }
}
</script>

[radio单选](https://v2.avuejs.com/component/radio/) [switch开关](https://v2.avuejs.com/component/switch/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
查看 Vue 3.x 的升级版本

关注Avue Cloud公众号