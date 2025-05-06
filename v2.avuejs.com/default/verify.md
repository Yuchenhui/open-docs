Verify 验证码
==========

结合video组件来做一些活体认证，或则是其他方面的验证

Tips

2.1.0

随机验证码  
请使用普通话朗读下方验证码  
  
<el-button @click="$refs.verify.randomn()" type="primary">随机验证码</el-button><br /><br />
<span style="font-size: 24px;line-height: 24px;color: #333;">请使用普通话朗读下方验证码</span><br /><br />
<avue-verify v-model="data" :len="len" ref="verify"></avue-verify><br /><br />
<avue-video background="https://avuejs.com/images/face.png" @data-change="dataChange" ref="video"></avue-video>

<script>
export default {
  data(){
    return {
      data:null,
      len:6,
    }
  },
  methods:{
    dataChange(data) {
      console.log(data);
    }
  }
}
</script>

[Video 摄像头](https://v2.avuejs.com/default/video/) [Print打印](https://v2.avuejs.com/default/print/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号