Clipboard 复制剪切板
===============

Tips

1.0.6+

直接复制 清 空

复制

```html
<div style="width:400px">
  <div style="margin-bottom:10px">
    <el-button @click="copy">直接复制</el-button>
    <el-button @click="textarea=''">清 空</el-button>
  </div>
  <el-input placeholder="内容" v-model="text">
    <template slot="append">
      <el-button @click="copyText" color="primary">复制</el-button>
    </template>
  </el-input>
  <div style="margin-top:10px">
    <el-input type="textarea" v-model="textarea" cols="40" rows="3"></el-input>
  </div>
</div>
<script>
export default {
  data() {
    return {
      text: '',
      textarea: ''
    }
  },
  methods: {
    copyText() {
      this.$Clipboard({
        text: this.text
      }).then(() => {
        this.$message.success('复制成功')
      }).catch(() => {
        this.$message.error('复制失败')
      });
    },
    copy() {
      this.$Clipboard({
        text: '测试==复制至剪切板的文本==测试'
      }).then(() => {
        this.$message.success('复制成功')
      }).catch(() => {
        this.$message.error('复制失败')
      });
    }
  }
}
</script>
```

Variables
---------

| 参数 | 说明   | 类型   | 可选值 | 默认值 |
| ---- | ------ | ------ | ------ | ------ |
| text | 复制的文本 | String | -      | -      |

[ImageCrooper 图片裁剪](https://v2.avuejs.com/default/image-cropper/) [Watermark 水印](https://v2.avuejs.com/default/watermark/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本 关注Avue Cloud公众号