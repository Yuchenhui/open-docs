Sign 电子签名
=========

兼容移动端和pc段

Tips

2.0.4+

生成 图章 清空

结果 ![](https://v2.avuejs.com/default/sign/)

```vue
<avue-sign ref="sign"></avue-sign>
<el-button type="primary" @click="handleSubmit">生成</el-button>
<el-button type="danger" @click="$refs.sign.getStar('这里是用途','这里是单位的名称','123456')">图章</el-button>
<el-button @click="$refs.sign.clear()">清空</el-button>
<div>
  <br />
  结果
  <img :src="img" alt="" width="80" height="50" />
</div>

<script>
export default {
  data() {
    return {
      img: ''
    }
  },
  methods: {
    handleSubmit() {
      this.img = this.$refs.sign.submit(80, 50);
      console.log(this.img)
    }
  }
}
</script>
```

[License 授权书](https://v2.avuejs.com/default/license/) [Flow 流程](https://v2.avuejs.com/default/flow/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号