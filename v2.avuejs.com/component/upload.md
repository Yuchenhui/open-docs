upload 附件上传
===========

值:[]

值:  

值:[]

<el-row :span="24">
  <el-col :span="6">
    值:{{form}}<br />
    <avue-upload
      :action="action"
      :props-http="propsHttp"
      type="upload"
      v-model="form"
    ></avue-upload>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    值:{{form1}}<br />
    <avue-upload
      :action="action"
      :props-http="propsHttp"
      type="upload"
      v-model="form1"
      list-type="picture-img"
    ></avue-upload>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    值:{{form2}}<br />
    <avue-upload
      :action="action"
      :props-http="propsHttp"
      type="upload"
      v-model="form2"
      list-type="picture-card"
    ></avue-upload>
  </el-col>
</el-row>
<script>
  export default {
    data() {
      return {
        action: "https://api.avuejs.com/imgupload",
        propsHttp: {
          url: "url",
          name: "name",
          res: "data",
        },
        form: [],
        form1: "",
        form2: [],
      };
    },
  };
</script>