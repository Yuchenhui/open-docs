slider滑动框
=========

值:52  

    <el-row :span="24">
      <el-col :span="6">
       值:{{form}}<br/>
       <avue-slider v-model="form" :max="100" :min="20"></avue-slider>
      </el-col>
    </el-row>
    <script>
    export default {
        data() {
          return {
            form:52
          }
        }
    }
    </script>

[rate评价框](https://v2.avuejs.com/component/rate/) [cascader级联选择器](https://v2.avuejs.com/component/cascader/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号