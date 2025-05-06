radio单选
=======

值:0  

    <el-row :span="24">
      <el-col :span="6">
       值:{{form}}<br/>
       <avue-radio v-model="form"  :dic="dic"></avue-radio>
      </el-col>
    </el-row>
    <script>
    export default {
        data() {
          return {
            form:0,
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

[select选择框](https://v2.avuejs.com/component/select/) [checkbox多选](https://v2.avuejs.com/component/checkbox/)