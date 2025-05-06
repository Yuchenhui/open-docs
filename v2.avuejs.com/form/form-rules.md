表单验证
====

基础用法
--------------------------------------------------------------------------------------

Tips

具体参考[async-validator (opens new window)](https://github.com/yiminghe/async-validator)

配置验证字段的`rules`的数据对象

```vue
<avue-form :option="option" @submit="submit" @error="error"></avue-form>

<script>
export default {
    data() {
      return {
        option:{
          column:[
             {
              label:'姓名',
              prop:'name',
              rules: [{
                required: true,
                message: "请输入姓名",
                trigger: "blur"
              }]
            }, {
              label:'性别',
              prop:'sex',
              rules: [{
                required: true,
                message: "请输入性别",
                trigger: "blur"
              }]
            }
          ]
        },
      };
    },
    methods: {
      submit(form,done){
        this.$message.success(JSON.stringify(form));
        done()
      },
      error(err){
        this.$message.success('请查看控制台');
        console.log(err)
      }
    }
}
</script>
```

外置验证
--------------------------------------------------------------------------------------

验证表单

```vue
<el-button size="small" @click="validate">验证表单</el-button>
<avue-form ref="form" :option="option" ></avue-form>

<script>
export default {
    data() {
      return {
        option:{
          column:[
             {
              label:'姓名',
              prop:'name',
              rules: [{
                required: true,
                message: "请输入姓名",
                trigger: "blur"
              }]
            }, {
              label:'性别',
              prop:'sex',
              rules: [{
                required: true,
                message: "请输入性别",
                trigger: "blur"
              }]
            }
          ]
        },
      };
    },
    methods: {
      validate(){
        //如果存在验证不通过，msg为错误信息
        this.$refs.form.validate((valid, done, msg) => {
          if (valid) {
            done()
          } else {
            console.log('error submit!!');
            return false;
          }
        })
      }
    }
}
</script>
```

自定义验证
------------------------------------------------------------------------------------------------

```vue
<avue-form  v-model="obj" :option="option1" @submit="submit" @error="error"></avue-form>

<script>
export default {
  data() {
    var validatePass = (rule, value, callback)=>{
      if (value === '') {
        callback(new Error('请输入密码'));
      } else {
        callback();
      }
    };
    var validatePass2 = (rule, value, callback)=>  {
      if (value === '') {
        callback(new Error('请再次输入密码'));
      } else if (value !== this.obj.password) {
        callback(new Error('两次输入密码不一致!'));
      } else {
        callback();
      }
    };
    return {
      obj:{
        name:'张三',
      },
      option1:{
        column:[
          {
            label:'姓名',
            prop:'name',
            rules: [{
              required: true,
              message: "请输入姓名",
              trigger: "blur"
            }]
          }, {
            label:'性别',
            prop:'sex',
            rules: [{
              required: true,
              message: "请输入性别",
              trigger: "blur"
            }]
          },
          {
            label:'密码',
            prop:'password',
            type:'password',
            rules: [{ validator: validatePass, trigger: 'blur' }]
          }, {
            label:'确认密码',
            prop:'oldpassword',
            type:'password',
            rules: [{ validator: validatePass2, trigger: 'blur' }]
          }
        ]
      },
    }
  },
  methods: {
    submit(form,done){
      this.$message.success(JSON.stringify(form));
      done()
    },
    error(err){
      this.$message.success('请查看控制台');
      console.log(err)
    }
  }
}
</script>
```

[表单布局](https://v2.avuejs.com/form/form-layout/) [表单默认值](https://v2.avuejs.com/form/form-value/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/) ** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号