input输入框
========

值:我是内容  

    <el-row :span="24">
      <el-col :span="6">
         值:{{form}}<br/>
        <avue-input v-model="form" placeholder="请输入内容" ></avue-input>
      </el-col>
    </el-row>
    <script>
    export default {
        data() {
          return {
            form:'我是内容'
          }
        }
    }
    </script>