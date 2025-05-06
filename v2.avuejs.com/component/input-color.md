inputColor颜色选择器
===============

值:rgba(255, 120, 0, 1)  值:#AE4141  

<el-row :span="24">
  <el-col :span="6">
   值:{{form}}<br/>
   <avue-input-color  placeholder="请选择颜色" v-model="form" ></avue-input-color>
  </el-col>
   <el-col :span="24"></el-col>
   <el-col :span="6">
   值:{{form1}}<br/>
   <avue-input-color color-format="hex" :show-alpha="false" placeholder="请选择颜色" v-model="form1" ></avue-input-color>
  </el-col>
</el-row>
<script>
export default {
    data() {
      return {
        form:'rgba(255, 120, 0, 1)',
        form1:'#AE4141'
      }
    }
}
</script>