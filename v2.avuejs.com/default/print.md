Print打印
=======

Tips

2.8.6+

打印全部 打印局部 打印DOM

我是测试字段
------

<el-button type="primary" @click="handlePrint">打印全部</el-button>
<el-button type="primary" @click="handlePrint1">打印局部</el-button>
<el-button type="primary" @click="handlePrint2">打印DOM</el-button>
<div id="test">
  <h2 style="color:red">我是测试字段</h2>
</div>
<script>
export default {
  methods: {
    handlePrint() {
      this.$Print('#app');
    },
    handlePrint1(){
      this.$Print('#test');
    },
    handlePrint2(){
      this.$Print(document.querySelector('.logo'));
    }
  }
}
</script>

Variables
--------------------------------------------------------------

| 参数  | 说明      | 类型   | 可选值 | 默认值 |
| ----- | --------- | ------ | ------ | ------ |
| id    | dom元素的id | String | -      | -      |
| html  | html代码片段 | String | -      | -      |

[Verify 验证码](https://v2.avuejs.com/default/verify/) [NProgress 进度条](https://v2.avuejs.com/default/nprogress/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号