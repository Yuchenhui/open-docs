Screenshot 屏幕截图
===============

Tips

2.1.1+

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里）-->
<script src="https://cdn.staticfile.net/html2canvas/0.5.0-beta4/html2canvas.min.js"></script>
```

意见反馈

```vue
<el-button @click="handleOk" type="primary" icon="el-icon-camera">意见反馈</el-button>
<el-dialog modal-append-to-body append-to-body title="意见反馈" top="50px" :visible.sync="box" width="60%">
  <el-input type="textarea" placeholder="请告诉我们遇到的问题或建议" v-model="form.text"></el-input>
  <br /><br />
  <div v-loading="flag" element-loading-text="正在截取屏幕数据">
    <img :src="form.img" width="100%" />
  </div>
  <span slot="footer">
    <el-button type="primary" icon="el-icon-check" @click="handleSubmit">提 交</el-button>
  </span>
</el-dialog>

<script>
export default {
  data() {
    return {
      box: false,
      form: {
        img: '',
        text: ''
      }
    };
  },
  computed: {
    flag() {
      return this.form.img;
    }
  },
  methods: {
    handleOk() {
      this.form = {
        img: '',
        text: ''
      };
      this.$Screenshot(document.querySelector("#app")).then(canvas => {
        this.form.img = canvas.toDataURL("image/jpeg", 0.8);
      });
      this.box = true;
    }
  }
};
</script>
```