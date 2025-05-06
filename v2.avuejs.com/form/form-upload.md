Upload 附件上传
===========

```js
//使用上传附件需要引入axios
import axios from "axios";
Vue.use(Avue, { axios });
```

Tips

`propsHttp`配置请求接口返回的数据结构  
- `name` 图片的名称  
- `url` 路径地址  
- `res` 返回数据层级结构  
- `home` 相对路径的主路径  

类型
----

`listType` 配置上传的类型, `multiple` 是否多选上传

```vue
<avue-form :option="option" v-model="form"></avue-form>

<script>
let action = "https://api.avuejs.com/imgupload";
export default {
  data() {
    return {
      form: {
        video: "/i/movie.ogg",
        imgUrl: [
          "/images/logo-bg.jpg",
          "https://www.w3school.com.cn/i/movie.ogg",
          "https://www.runoob.com/try/demo_source/horse.mp3",
        ],
      },
      option: {
        column: [
          {
            label: "附件上传",
            prop: "imgUrl",
            type: "upload",
            multiple: true,
            span: 24,
            propsHttp: {
              url: "url",
              name: "name",
              res: "data",
            },
            action: action,
          },
          {
            label: "视频",
            prop: "video",
            type: "upload",
            propsHttp: {
              res: "data",
              url: "url",
              name: "name",
              home: "https://www.w3school.com.cn",
            },
            listType: "picture-img",
            span: 24,
            action: action,
          },
          {
            label: "照片墙",
            prop: "imgUrl",
            listType: "picture-card",
            type: "upload",
            span: 24,
            propsHttp: {
              res: "data",
            },
            action: action,
          },
          {
            label: "缩略图上传",
            prop: "imgUrl",
            type: "upload",
            span: 24,
            propsHttp: {
              res: "data",
            },
            listType: "picture",
            action: action,
          },
          {
            label: "拖拽上传",
            prop: "imgUrl",
            type: "upload",
            propsHttp: {
              res: "data",
            },
            span: 24,
            dragFile: true,
            action: action,
          },
        ],
      },
    };
  },
};
</script>
```

数据类型
-------

Tips

`dataType` 配置数据的结构 `string`、`object`、`json` 当 `dataType` 配置为 `object` 时，可以配置 `props` 存储的数据结构  

- `label` 图片的名称  
- `value` 路径地址  

当 `dataType` 配置为 `json` 时，是 json 序列化字符串, 也可以配置 `props` 存储的数据结构

```vue
<avue-form :option="option" v-model="form"> </avue-form>

<script>
export default {
  data() {
    return {
      form: {
        array: [{ label: "名称.jpg", value: "/images/logo-bg.jpg" }],
        array1: [{ name: "名称.jpg", url: "/images/logo-bg.jpg" }],
        string: "/images/logo-bg.jpg,/images/logo-bg.jpg",
        json: '[{"label":"名称.jpg","value":"/images/logo-bg.jpg"}]',
      },
      option: {
        labelWidth: 120,
        column: [
          {
            label: "数组对象",
            prop: "array",
            dataType: "object",
            type: "upload",
            propsHttp: {
              res: "data",
            },
            span: 24,
            action: "https://api.avuejs.com/imgupload",
          },
          {
            label: "数组对象",
            prop: "array1",
            dataType: "object",
            type: "upload",
            props: {
              label: "name",
              value: "url",
            },
            propsHttp: {
              res: "data",
            },
            span: 24,
            action: "https://api.avuejs.com/imgupload",
          },
          {
            label: "字符串",
            prop: "string",
            dataType: "string",
            type: "upload",
            propsHttp: {
              res: "data",
            },
            span: 24,
            action: "https://api.avuejs.com/imgupload",
          },
          {
            label: "json字符串",
            prop: "json",
            dataType: "json",
            type: "upload",
            propsHttp: {
              res: "data",
            },
            span: 24,
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

上传前和上传后方法
---------------

`upload-before` 上传前的回调, `upload-after` 上传后的回调

```vue
<avue-form
  :option="option"
  v-model="form"
  :upload-before="uploadBefore"
  :upload-after="uploadAfter"
></avue-form>

<script>
export default {
  data() {
    return {
      form: {
        imgUrl: ["/images/logo-bg.jpg"],
      },
      option: {
        column: [
          {
            label: "附件上传",
            prop: "imgUrl",
            type: "upload",
            listType: "picture-card",
            span: 24,
            propsHttp: {
              res: "data",
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
  methods: {
    uploadBefore(file, done, loading, column) {
      console.log(file, column);
      //如果想修改file文件，由于上传的file是只读文件，必须复制新的file才可以修改名字，完后赋值到done函数里，如果不修改的话直接写done()即可
      var newFile = new File([file], "1234", { type: file.type });
      done(newFile);
      this.$message.success("上传前的方法");
    },
    uploadAfter(res, done, loading, column) {
      console.log(res, column);
      done();
      this.$message.success("上传后的方法");
    },
  },
};
</script>
```

自定义预览方法
------------

配置 `uploadPreview` 预览回调方法

```vue
<avue-form
  :option="option"
  v-model="form"
  :upload-preview="uploadPreview"
></avue-form>

<script>
export default {
  data() {
    return {
      form: {
        imgUrl: [
          "/images/logo-bg.jpg",
          "https://www.w3school.com.cn/i/movie.ogg",
        ],
      },
      option: {
        column: [
          {
            label: "附件上传",
            prop: "imgUrl",
            type: "upload",
            listType: "picture-card",
            span: 24,
            propsHttp: {
              res: "data",
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
  methods: {
    uploadPreview(file, column, done) {
      this.$confirm("是否放大查看图片").then(() => {
        done(); //默认执行打开方法
      });
    },
  },
};
</script>
```

自定义删除方法
------------

配置 `uploadDelete` 删除回调函数

```vue
<avue-form :option="option" v-model="form" :upload-delete="uploadDelete">
</avue-form>

<script>
export default {
  data() {
    return {
      form: {
        imgUrl3: ["/images/logo-bg.jpg"],
      },
      option: {
        column: [
          {
            label: "水印头像",
            prop: "imgUrl3",
            type: "upload",
            listType: "picture-card",
            span: 24,
            propsHttp: {
              res: "data",
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
  methods: {
    uploadDelete(file, column) {
      console.log(file, column);
      return this.$confirm("这里是自定义的，是否确定移除该选项？");
    },
  },
};
</script>
```

指定文件类型
------------

可以配置 `fileType` 来指定文件的类型，一般用于没有后缀格式的地址

```vue
<avue-form :option="option" v-model="form"> </avue-form>

<script>
export default {
  data() {
    return {
      form: {
        imgUrl3: "https://www.runoob.com/try/demo_source/circle1.svg",
      },
      option: {
        column: [
          {
            label: "头像",
            prop: "imgUrl3",
            type: "upload",
            listType: "picture-img",
            span: 24,
            fileType: "img", // img/video/audio
            propsHttp: {
              res: "data",
            },
            tip: "只能上传jpg/png用户头像，且不超过500kb",
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

传参
----

可以配置 `data` 和 `headers` 属性作为传递参数

```vue
<avue-form :option="option" v-model="form"> </avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "头像",
            prop: "imgUrl3",
            type: "upload",
            listType: "picture-img",
            span: 24,
            propsHttp: {
              res: "data",
            },
            data: {
              a: 1,
            },
            headers: {
              b: 1,
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

上传等待文案和按钮文案
-----------------

可以配置 `loadText` 上传等待文案, `fileText` 上传按钮文案, `tip` 提示文案

```vue
<avue-form :option="option" v-model="form"> </avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "头像",
            prop: "imgUrl3",
            type: "upload",
            span: 24,
            propsHttp: {
              res: "data",
            },
            fileText: "我是上传按钮",
            loadText: "上传等待文案",
            tip: "只能上传jpg/png用户头像，且不超过500kb",
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

限制文件类型和大小数量
-------------------

可以配置 `accept` 限制格式和 `limit` 显示个数以及 `fileSize` 限制大小对应参数即可, `fileSize` 对应基础单位为 KB

```vue
<avue-form :option="option" v-model="form" :upload-sized="uploadSized">
</avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "水印头像",
            prop: "imgUrl3",
            type: "upload",
            listType: "picture-card",
            accept: "image/png, image/jpeg",
            limit: 2,
            fileSize: 10000,
            span: 24,
            propsHttp: {
              res: "data",
            },
            tip: "只能上传jpg/png用户头像，且不超过10M",
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
  methods: {
    uploadSize(fileSize, files, fileList, column) {
      console.log(fileSize, files, fileList, column);
      this.$message.error("超出上传限制大小");
    },
  },
};
</script>
```

超出上传限制回调
-------------

`uploadExceed` 文件超出上传限制回调

```vue
<avue-form
  :option="option"
  v-model="form"
  :upload-exceed="uploadExceed"
></avue-form>

<script>
export default {
  data() {
    return {
      form: {
        imgUrl: ["/images/logo-bg.jpg"],
      },
      option: {
        column: [
          {
            label: "附件上传",
            prop: "imgUrl",
            type: "upload",
            listType: "picture-card",
            limit: 1,
            span: 24,
            propsHttp: {
              res: "data",
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
  methods: {
    uploadExceed(limit, files, fileList, column) {
      console.log(limit, files, fileList, column);
      this.$message.error("超出上传限制文件数量");
    },
  },
};
</script>
```

上传失败错误回调函数
---------------

`uploadError` 上传失败错误回调函数

```vue
<avue-form
  :option="option"
  v-model="form"
  :upload-error="uploadError"
></avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        labelWidth: 120,
        column: [
          {
            label: "附件上传",
            prop: "imgUrl",
            type: "upload",
            listType: "picture-card",
            span: 24,
            propsHttp: {
              res: "data",
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
  methods: {
    uploadError(error, column) {
      this.$message.success("上传失败回调");
      console.log(error, column);
    },
  },
};
</script>
```

自定义模板
--------

列名的 `prop` 加上 `Type` 即可自定义内容

```vue
<avue-form :option="option" v-model="form">
  <template slot="imgUrlType" slot-scope="{file}">
    <span>自定义模板{{file}}</span>
  </template>
</avue-form>

<script>
export default {
  data() {
    return {
      form: {
        imgUrl: [
          "/images/logo-bg.jpg",
          "https://www.w3school.com.cn/i/movie.ogg",
        ],
      },
      option: {
        column: [
          {
            label: "附件上传",
            prop: "imgUrl",
            type: "upload",
            span: 24,
            propsHttp: {
              res: "data",
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

图片水印
------

可以配置 `canvasOption` 属性去生成水印和压缩图片，

```vue
<avue-form :option="option" v-model="form"> </avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "水印头像",
            prop: "imgUrl3",
            type: "upload",
            listType: "picture-img",
            span: 24,
            propsHttp: {
              res: "data",
            },
            canvasOption: {
              text: "avue",
              ratio: 0.1,
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

图片裁剪
------

可以配置 `cropperOption` 属性去配置图片裁剪参数

```vue
<avue-form :option="option" v-model="form"> </avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "图片裁剪",
            prop: "imgUrl3",
            type: "upload",
            listType: "picture-img",
            span: 24,
            propsHttp: {
              res: "data",
            },
            cropperOption: {
              autoCropWidth: 100,
              autoCropHeight: 100,
              fixed: true,
              fixedNumber: [100, 100],
            },
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

拖拽排序
------

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<script src="https://cdn.staticfile.net/Sortable/1.10.0-rc2/Sortable.min.js"></script>
```

配置 `drag` 属性即可开启拖拽排序

```vue
{{form}}
<avue-form :option="option" v-model="form"> </avue-form>
<script>
export default {
  data() {
    return {
      form: {
        img: ["/images/logo-bg.jpg", "/images/logo-bg.jpg", "./xx/xx.sql"],
      },
      option: {
        labelWidth: 120,
        column: [
          {
            label: "数组图片组",
            prop: "img",
            drag: true,
            type: "upload",
            propsHttp: {
              res: "data",
            },
            span: 24,
            listType: "picture-card",
            action: "https://api.avuejs.com/imgupload",
          },
        ],
      },
    };
  },
};
</script>
```

阿里云 oss 上传
---------

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<script src="https://cdn.staticfile.net/ali-oss/6.10.0/aliyun-oss-sdk.min.js"></script>
```

```js
//入口处全局配置阿里云的参数
Vue.use(AVUE, {
  ali: {
    region: "oss-cn-beijing",
    endpoint: "oss-cn-beijing.aliyuncs.com",
    stsToken: "",
    accessKeyId: "",
    accessKeySecret: "",
    bucket: "avue",
  },
});
```

```vue
<avue-form :option="option" v-model="form"> </avue-form>
<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "阿里上传",
            prop: "imgUrl",
            type: "upload",
            listType: "picture-img",
            canvasOption: {
              text: "avue",
              ratio: 0.1,
            },
            oss: "ali",
            span: 24,
          },
        ],
      },
    };
  },
};
</script>
```

七牛云 oss 上传
----------

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<script src="https://avuejs.com/cdn/CryptoJS.js"></script>
```

```js
Vue.use(AVUE, {
  qiniu: {
    AK: '', //七牛云相关密钥
    SK: '', //七牛云相关密钥
    bucket:'https://upload.qiniup.com', //存储地区，默认为华东，其他的如下表
    scope: 'test', //存储空间名称
    url: 'https://cdn.avuejs.com/' //外链的域名地址
  }
})
```

```vue
<avue-form :option="option" v-model="form"> </avue-form>
<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "七牛上传",
            prop: "imgUrl",
            type: "upload",
            listType: "picture-img",
            fileType: "img",
            oss: "qiniu",
            span: 24,
          },
        ],
      },
    };
  },
};
</script>
```

腾讯云 oss 上传
----------

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<script src="https://avuejs.com/cdn/cos-js-sdk-v5.min.js"></script>
```

```js
Vue.use(AVUE, {
  cos: {
    SecretId: "", //腾讯云相关密钥
    SecretKey: "", //腾讯云相关密钥
    Bucket: "test", //存储空间名称
    Region: "ap-beijing", //存储地区
  },
});
```

```vue
<avue-form :option="option" v-model="form"> </avue-form>
<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [
          {
            label: "腾讯上传",
            prop: "imgUrl",
            type: "upload",
            listType: "picture-img",
            fileType: "img",
            oss: "cos",
            span: 24,
          },
        ],
      },
    };
  },
};
</script>
```