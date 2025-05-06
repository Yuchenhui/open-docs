inputNumber数字框
==============

值:1  
值:1  
有最小最大值的数据:1  

<el-row :span="24">
  <el-col :span="6">
   值:{{form}}<br/>
   <avue-input-number v-model="form"></avue-input-number>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
   值:{{form}}<br/>
    <avue-input-number v-model="form" precision="2" controls-position=""></avue-input-number>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    有最小最大值的数据:{{hasMinMaxForm}}<br/>
    <avue-input-number v-model="hasMinMaxForm" precision="2" controls-position="" :min="min" :max="max"></avue-input-number>
  </el-col>
</el-row>

<script>
export default {
    data() {
      return {
        form:1,
        hasMinMaxForm: 1,
        min: 0, // 最小值
        max: 10 // 最大值
      }
    }
}
</script>