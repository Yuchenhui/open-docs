Watermark 水印
============

Tips

2.0.1+

全局水印 局部水印 删除水印  

```html
<div style="width:400px">
  <el-button @click="submit" type="primary">全局水印</el-button>
  <el-button @click="submit1" type="primary">局部水印</el-button>
  <el-button @click="del" type="danger">删除水印</el-button>
  <br /> <br />
  <div id="test" style="width:300px;height:300px;border:1px solid #ccc;position:relative;"></div>
</div>
<script>
export default {
  data(){
    return {
      obj:'',
      obj1:'',
      create:false
    }
  },
  methods: {
      submit() {
        if(this.create){
          this.$message.success('已经创建水印了')
          return 
        }
        this.create=true;
        this.$message.success('添加水印成功')
        this.obj=this.watermark({text:'avue全局水印'})
      },
      submit1() {
        this.obj1=this.watermark({
          id:'test',
          fontSize:'14px',
          width:'100',
          height:'80',
          text:'avue局部水印'
        })
      },
      del(){
        this.obj.remove();
        this.obj1.remove();
        this.create=false;
      },
  }
}
</script>
```

Variables
---------

| 参数     | 说明       | 类型   | 可选值 | 默认值                  |
| -------- | ---------- | ------ | ------ | ----------------------- |
| text     | 文字内容   | String | -      | avue商用通用无敌大水印 |
| fontSize | 字体大小   | String | -      | 30px                    |
| fontStyle| 字体类型   | String | -      | 黑体                    |
| width    | 字体的宽度 | String | -      | 200                     |
| height   | 字体的高度 | String | -      | 400                     |
| color    | 字体颜色   | String | -      | rgba(100,100,100,0.15)  |
| degree   | 文本旋转角度| String | -      | -20                     |

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/) 查看 Vue 3.x 的升级版本**

关注Avue Cloud公众号