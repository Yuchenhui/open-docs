DialogForm弹窗表单
==============

Tips

2.9.0+

更多Form配置属性可以参考[From组件文档](https://v2.avuejs.com/form/form)

弹窗表单 抽屉表单 弹窗表单（带上数据）

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