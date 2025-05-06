inputTree树型组件
=============

值:  
包含父类值:[ 0, 1, 2, 3, 4 ]  
不包含父类值:[ 1, 2, 3 ]  
半选是否包含父类值:[]  
半选是不包含父类值:[ 2, 1 ]  
父子不关联:[ 0 ]  

```vue
<el-row :span="24">
  <el-col :span="6">
     值:{{form}}<br/>
    <avue-input-tree default-expand-all v-model="form" placeholder="请选择内容" :dic="dic"></avue-input-tree>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
     包含父类值:{{form1}}<br/>
    <avue-input-tree multiple v-model="form1" placeholder="请选择内容"  :dic="dic"></avue-input-tree>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
     不包含父类值:{{form2}}<br/>
    <avue-input-tree leaf-only multiple v-model="form2" placeholder="请选择内容"  :dic="dic"></avue-input-tree>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
     半选是否包含父类值:{{form33}}<br/>
     半选是不包含父类值:{{form3}}<br/>
    <avue-input-tree ref="tree" include-half-checked multiple v-model="form3" placeholder="请选择内容" :dic="dic"></avue-input-tree>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
     父子不关联:{{form4}}<br/>
    <avue-input-tree :check-strictly="true" multiple v-model="form4" placeholder="请选择内容"  :dic="dic"></avue-input-tree>
  </el-col>
</el-row>

<script>
export default {
  data() {
    return {
      form: '',
      form1: [0, 1, 2, 3, 4],
      form2: [1, 2, 3],
      form3: [2, 1],
      form33: [],
      form4: [0],
      dic: [
        {
          label: '选项1',
          value: 0,
          children: [
            {
              label: '选项3',
              value: 2
            },
            {
              label: '选项4',
              value: 3
            }
          ]
        },
        {
          label: '选项2',
          value: 1
        }
      ]
    }
  },
  watch: {
    form3: {
      handler() {
        this.form33 = this.$refs.tree.getHalfList();
      }
    }
  },
  mounted() {
    this.form33 = this.$refs.tree.getHalfList();
  }
}
</script>
```