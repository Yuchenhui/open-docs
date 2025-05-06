rate评价框
=======

值:4  

<el-row :span="24">
  <el-col :span="6">
    值:{{form}}<br/>
    <avue-rate v-model="form"></avue-rate>
  </el-col>
</el-row>
<script>
export default {
  data() {
    return {
      form: 4
    }
  }
}
</script>

[time时间](https://v2.avuejs.com/component/time/) [slider滑动框](https://v2.avuejs.com/component/slider/)