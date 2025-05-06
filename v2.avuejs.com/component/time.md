time时间
======

... 2022-9-15 Less than 1 minute

* * *

[#](https://v2.avuejs.com/component/time/#time%E6%97%B6%E9%97%B4)
time时间
=========================================================================

值:12:00:00  

<el-row :span="24">
  <el-col :span="6">
   值:{{form}}<br/>
   <avue-time v-model="form" format="hh时mm分ss秒" value-format="hh:mm:ss" placeholder="请选择时间"></avue-time>
  </el-col>
</el-row>
<script>
export default {
    data() {
      return {
        form:'12:00:00'
      }
    }
}
</script>

[datetime日期时间](https://v2.avuejs.com/component/datetime/) [rate评价框](https://v2.avuejs.com/component/rate/)

Install Cancel

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
查看 Vue 3.x 的升级版本

关注Avue Cloud公众号