表单默认值
=====

表单默认值
================================================================================================

配置方法
--------------------------------------------------------------------------------------

配置`value`为字段默认值

    <avue-form :option="option" v-model="form" > </avue-form>
    
    <script>
    export default{
      data() {
        return {
          form: {},
          option: {
            column: [
              {
                label: '姓名',
                prop: 'name',
                value:'small'
              }
            ]
          }
        }
      }
    }
    </script>

赋值方法
--------------------------------------------------------------------------------------

改变值  
  

利用`v-model`绑定的对象直接操作即可

    <el-button @click="changeText" size="small" type="success">改变值</el-button>
    <br/><br/>
    <avue-form :option="option" v-model="form" > </avue-form>
    
    <script>
    export default{
      data() {
        return {
          form: {
            name:'small'
          },
          option: {
            column: [
              {
                label: '姓名',
                prop: 'name'
              }
            ]
          }
        }
      },
      methods:{
          changeText(){
            this.form.name="我改变了"
          }
      }
    }
    </script>

[表单验证](https://v2.avuejs.com/form/form-rules/) [表单操作按钮](https://v2.avuejs.com/form/form-submit/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号