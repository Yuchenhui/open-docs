全局配置
====

在引入 Avue 时，可以传入一个全局配置对象

```javascript
Vue.use(AVUE,{
  size:'',
  crudOption:{},
  formOption:{},
  tableSize:'',
  formSize:'',
  appendToBody:true,
  modalAppendToBody:true,
  cos:{},
  qiniu:{},
  ali:{},
  canvas:{}
});
```

* size：用于改变组件的默认尺寸，属性的组件的默认尺寸均为 `small`。可选值`small`/`mini`/`medium`;
* crudOption：全局Crud组件的默认配置

```javascript
{
  index:true,
  indexLabel:'序号',
  ....
}
```

* formOption：全局Form组件的默认配置

```javascript
{
  labelWidth:110,
  ....
}
```

* qiniu 七牛云配置

```javascript
{
  AK: '',
  SK: '',
  scope: '',
  url: '',
  deadline: 1
}
```

* ali 阿里云配置

```javascript
{
  region: '',
  endpoint: '',
  accessKeyId: '',
  accessKeySecret: '',
  bucket: '',
}
```

* cos 腾讯云配置

```javascript
{
  SecretId: '',
  SecretKey: '',
  Bucket: '',
  Region: ''
}
```

* canvas 全局水印配置

```javascript
{
  text: 'avuejs.com',
  fontFamily: 'microsoft yahei',
  color: "#999",
  fontSize: 16,
  opacity: 100,
  bottom: 10,
  right: 10,
  ratio: 1
}
```

[快速上手](https://v2.avuejs.com/docs/installation/) [国际化](https://v2.avuejs.com/docs/locale/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号