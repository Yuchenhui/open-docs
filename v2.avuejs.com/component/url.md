url超链接输入框
=========

值:["https://avuejs.com/"]

```vue
<el-row :span="24">
  <el-col :span="6">
    值:{{form}}<br/>
    <avue-array type="url" alone v-model="form" placeholder="请输入内容"></avue-array>
  </el-col>
</el-row>
<script>
export default {
  data() {
    return {
      form: ['https://avuejs.com/']
    }
  }
}
</script>
```

[img图片输入框](https://v2.avuejs.com/component/img/) [select选择框](https://v2.avuejs.com/component/select/)