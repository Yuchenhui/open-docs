表单高级用法
======

表单初始化
-----------------------------------------------------------------------------------------------

Key初始化

```vue
<el-button type="primary" size="small" @click="handleReload" >Key初始化</el-button>
<avue-form :key="reload"  :option="option" ></avue-form>

<script>
export default {
    data() {
      return {
        reload: Math.random(),
        option:{
          border:true,
          align:'center',
          menuAlign:'center',
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            },{
              label: '省份',
              prop: 'province',
              type: 'select',
              props: {
                label: 'name',
                value: 'code'
              },
              dicUrl: `https://cli.avuejs.com/api/area/getProvince`,
              rules: [
                {
                  required: true,
                  message: '请选择省份',
                  trigger: 'blur'
                }
              ]
            }]
          }
        }
    },
    methods:{
      handleReload(){
        this.reload=Math.random();
        this.$message.success('初始化完成')
      }
    }
}
</script>
```

配置项服务端加载
-----------------------------------------------------------------------------------------------------------------------------

Tips

*   这里没有走真真的服务器请求，而是做了一个模拟

服务端加载

```vue
<el-button type="primary"
            size="small"
            icon="el-icon-sort"
            @click="getOption">服务端加载</el-button>
<avue-form :key="reload" v-model="form" :option="option" v-loading="loading"></avue-form>

<script>
export default {
  data () {
    return {
      reload: Math.random(),
      loading: true,
      form: {},
      option: {},
    };
  },
  methods: {
    getOption () {
      this.$message.success('模拟2s后服务端动态加载');
      setTimeout(() => {
        this.option = {
          border: true,
          align: 'center',
          menuAlign: 'center',
          column: [
            {
              label: '姓名',
              prop: 'name'
            }, {
              label: '性别',
              prop: 'sex'
            }, {
              label: '省份',
              prop: 'province',
              type: 'select',
              props: {
                label: 'name',
                value: 'code'
              },
              dicUrl: `https://cli.avuejs.com/api/area/getProvince`,
              rules: [
                {
                  required: true,
                  message: '请选择省份',
                  trigger: 'blur'
                }
              ]
            }]
        }
        this.form = {
          name: '张三',
          sex: '男',
          province: '110000'
        }
         this.reload = Math.random()
        this.loading = false;

      }, 2000)
    }
  }
}
</script>
```

配置项切换
-----------------------------------------------------------------------------------------------

切 换  

```vue
<el-button type="primary" size="small" icon="el-icon-sort"  @click="handleSwitch" >切 换</el-button>
<br/><br/>
<avue-form :key="reload" v-model="form" :option="option">
</avue-form>

<script>
export default {
    data() {
      return {
        reload: Math.random(),
        type:true,
        form: {
          name:'张三',
          sex:'男',
          username:'smallwei',
          password:'smallwei'
        },
        option:{},
        option1:{
          addBtn:false,
          column:[
             {
              label:'昵称',
              prop:'name'
            }
          ]
        },
        option2:{
          addBtn:false,
          column:[
             {
              label:'用户名',
              prop:'username'
            }, {
              label:'密码',
              prop:'password',
              type:'password'
            }, {
              label:'姓名',
              prop:'name'
            }
          ]
        },
      };
    },
    mounted(){
      this.handleSwitch();
    },
    methods: {
      handleSwitch(){
        this.type=!this.type;
        if(this.type){
          this.option=this.option1;
        }else{
          this.option=this.option2;
        }
        this.reload=Math.random();
      }
    }
}
</script>
```

动态改变结构
---------------------------------------------------------------------------------------------------------

Tips

2.8.12+

```vue
<avue-form :defaults.sync="defaults" :option="option"  v-model="form"></avue-form>
<script>
export default {
  data(){
    return {
       defaults:{},
       form:{
          text1:0,
       },
       option:{
          column: [
            {
              label: '内容1',
              prop: 'text1',
              type:'radio',
              dicData:[
                {
                  label:'显示',
                  value:0
                },{
                  label:'隐藏',
                  value:1,
                }
              ]
            },{
              label: '内容2',
              prop: 'text2',
              display:true
            },{
              label: '内容3',
              prop: 'text3'
            }
          ]
       }
    }
  },
  watch:{
    'form.text1'(val){
      if(val==0){
        this.defaults.text2.display=true
        this.defaults.text3.label='内容3'
      }else{
        this.defaults.text2.display=false
        this.defaults.text3.label='有没有发现我变了'
      }
    }
  }
}
</script>
```

函数用法
-------------------------------------------------------------------------------------

Tips

2.9.0+

弹窗表单 抽屉表单 弹窗表单（带上数据）

```vue
<el-button type="primary" @click="showDialog"> 弹窗表单</el-button>
<el-button type="primary" @click="showDialog('drawer')"> 抽屉表单</el-button>
<el-button type="success" @click="showDialog1"> 弹窗表单（带上数据）</el-button>
<script>
export default {
  data() {
      return {
        option: {
          submitText: '完成',
          span:24,
          column: [
            {
              label: "姓名",
              prop: "name",
              rules: [{
                required: true,
                message: "请输入姓名",
                trigger: "blur"
              }],
            },
            {
              label: "年龄",
              prop: "age"
            }
          ]
        },
        form: {}
      }
    },
    methods: {
      showDialog(type) {
        this.$DialogForm.show({
          title: '弹窗页面',
          width: '30%',
          type:type,
          menuPosition:'right',
          option: this.option,
          beforeClose: (done) => {
            this.$message.success('关闭前方法')
            done()
          },
          callback:(res)=>{
            console.log(res.data);
            this.$message.success('关闭等待框')
            setTimeout(() => {
              res.done()
              setTimeout(() => {
                this.$message.success('关闭弹窗')
                res.close()
              }, 1000)
            }, 1000)
          }
        })

      },
      showDialog1() {
        this.$DialogForm.show({
          title: '弹窗页面（带上数据)',
          width: '50%',
          data: { name: 'small',age:18 },
          option: this.option,
          callback:(res)=>{
            console.log(res.data);
            this.$message.success('关闭等待框')
            setTimeout(() => {
              res.done()
              setTimeout(() => {
                this.$message.success('关闭弹窗')
                res.close()
              }, 1000)
            }, 1000)
          }
        })
      }
    }
  }
</script>
```

[表单组件事件](https://v2.avuejs.com/form/form-event/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号