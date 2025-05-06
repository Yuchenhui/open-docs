ImageCrooper 图片裁剪
=================

... 2022-6-2 About 3 min

可以裁剪图片地址或者Base64

Tips

2.9.9+

打开图片裁剪

![](https://v2.avuejs.com/images/logo.png)![](https://img.alicdn.com/tfs/TB1uevcCrj1gK0jSZFuXXcrHpXa-1880-640.jpg)![](https://img.alicdn.com/tfs/TB1v28TC8v0gK0jSZKbXXbK2FXa-1880-640.jpg)

### 裁剪图片

![](https://v2.avuejs.com/default/image-cropper/)

```vue
<div>
  <el-button @click="openPreview(0)" style="margin-bottom:20px;">打开图片裁剪</el-button>
  <p>
    <img width="200px" style="margin-right:20px" v-for="(d, index) of datas" :src="d.thumbUrl" @click="openPreview(index)">
  </p>
  <div>
    <h3> 裁剪图片</h3>
    <img :src="src" />
  </div>
</div>
<script>
export default {
  data() {
    return {
      src: '',
      datas: [
        { thumbUrl: `/images/logo.png`, url: `/images/logo.png` },
        { thumbUrl: `https://img.alicdn.com/tfs/TB1uevcCrj1gK0jSZFuXXcrHpXa-1880-640.jpg`, url: `https://img.alicdn.com/tfs/TB1uevcCrj1gK0jSZFuXXcrHpXa-1880-640.jpg` },
        { thumbUrl: `https://img.alicdn.com/tfs/TB1v28TC8v0gK0jSZKbXXbK2FXa-1880-640.jpg`, url: `https://img.alicdn.com/tfs/TB1v28TC8v0gK0jSZKbXXbK2FXa-1880-640.jpg` }
      ]
    }
  },
  methods: {
    openPreview(index = 0) {
      this.$ImageCropper({
        img: this.datas[index].thumbUrl,
        // autoCropWidth:100,
        // autoCropHeight:100,
        // fixed:true,
        // fixedNumber:[100,100],
        type: 'base64',
        callback: (res) => {
          console.log(res);
          this.src = res;
        },
        cancel: () => {
          this.$message.success('取消了');
        }
      });
    }
  }
}
</script>
```

Variables
---------

| 名称          | 功能                 | 默认值               | 可选值                           |
| ------------- | -------------------- | -------------------- | --------------------------------|
| img           | 裁剪图片的地址       | 空                   | url 地址 \| base64 \| blob       |
| type          | 裁剪图片返回格式     | base64               | base64 \| file                  |
| callback      | 裁剪图片成功回调     | 空                   | 空                              |
| cancel        | 裁剪图片取消回调     | 空                   | 空                              |
| outputSize    | 裁剪生成图片的质量   | 1                    | 0.1 - 1                        |
| outputType    | 裁剪生成图片的格式   | jpg (jpg 需要传入jpeg)| jpeg \| png \| webp             |
| info          | 裁剪框的大小信息     | true                 | true \| false                  |
| canScale      | 图片是否允许滚轮缩放 | true                 | true \| false                  |
| autoCrop      | 是否默认生成截图框   | false                | true \| false                  |
| autoCropWidth | 默认生成截图框宽度   | 容器的80%            | 0~max                          |
| autoCropHeight| 默认生成截图框高度   | 容器的80%            | 0~max                          |
| fixed         | 是否开启截图框宽高固定比例 | true           | true \| false                  |
| fixedNumber   | 截图框的宽高比例     | [1, 1]               | [宽度, 高度]                   |
| full          | 是否输出原图比例的截图 | false                | true \| false                  |
| fixedBox      | 固定截图框大小 不允许改变 | false             | true \| false                  |
| canMove       | 上传图片是否可以移动 | true                 | true \| false                  |
| canMoveBox    | 截图框能否拖动       | true                 | true \| false                  |
| original      | 上传图片按照原始比例渲染 | false              | true \| false                  |
| centerBox     | 截图框是否被限制在图片里面 | false             | true \| false                  |
| high          | 是否按照设备的dpr 输出等比例图片 | true          | true \| false                  |
| infoTrue      | true 为展示真实输出图片宽高 false 展示看到的截图框宽高 | false | true \| false          |
| maxImgSize    | 限制图片最大宽度和高度 | 2000                 | 0-max                         |
| enlarge       | 图片根据截图框输出比例倍数 | 1                 | 0-max (建议不要太大不然会卡死的呢) |
| mode          | 图片默认渲染方式     | contain              | contain , cover, 100px, 100% auto |

[ImagePreview 图片预览](https://v2.avuejs.com/default/image-preview/) [Clipboard 复制剪切板](https://v2.avuejs.com/default/clipboard/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号