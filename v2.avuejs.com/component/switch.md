switch开关
========

值:1 颜色值:1  图标值:1  

```vue
<el-row :span="24">
  <el-col :span="6">
   值:{{form}}<br/>
   <avue-switch v-model="form"  :dic="dic"></avue-switch>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
   颜色值:{{form}}<br/>
   <avue-switch active-color="#13ce66" inactive-color="#ff4949" v-model="form"  :dic="dic"></avue-switch>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
   图标值:{{form}}<br/>
   <avue-switch active-icon-class="el-icon-s-tools" inactive-icon-class="el-icon-setting" v-model="form"  :dic="dic"></avue-switch>
  </el-col>
</el-row>
<script>
export default {
  data() {
    return {
      form: 1,
      dic: [
        {
          label: '选项1',
          value: 0
        },
        {
          label: '选项2',
          value: 1
        }
      ]
    }
  }
}
</script>
```

[checkbox多选](https://v2.avuejs.com/component/checkbox/) [datetime日期时间](https://v2.avuejs.com/component/datetime/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号