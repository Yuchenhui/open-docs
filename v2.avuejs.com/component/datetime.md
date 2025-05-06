datetime日期时间
============

值:2020-01-01  
值:2020-01-01 12:00:00  

<el-row :span="24">
  <el-col :span="6">
    值:{{form}}<br/>
    <avue-date v-model="form" format="yyyy年MM月dd日" value-format="yyyy-MM-dd" placeholder="请选择日期"></avue-date> 
    <el-col :span="24"></el-col>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    值:{{form1}}<br/>
    <avue-date v-model="form1" type="datetime" format="yyyy年MM月dd日 hh:mm:ss" value-format="yyyy-MM-dd hh:mm:ss" placeholder="请选择日期"></avue-date>
  </el-col>
</el-row>
<script>
export default {
  data() {
    return {
      form:'2020-01-01',
      form1:'2020-01-01 12:00:00'
    }
  }
}
</script>

[switch开关](https://v2.avuejs.com/component/switch/) [time时间](https://v2.avuejs.com/component/time/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
查看 Vue 3.x 的升级版本

关注Avue Cloud公众号