表格错位问题
======

2022-4-25 Less than 1 minute

表格错位问题
=======================================================================================================

Tips

如果表格出现错位问题，是fixed冻结列导致的，去掉冻结列即可，或者参考表格初始化。

配置`indexFixed`、`selectionFixed`、`expandFixed`可以配置序号、多选、面板是否为冻结。

```vue
<avue-crud :data="data" :option="option" ></avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            id:1,
            name:'张三',
            sex:'男'
          }, {
            id:2,
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          index:true,
          indexFixed:false,
          // indexWidth:100,
          selection:true,
          // selectionWidth:100,
          selectionFixed:false,
          expand:true,
          // expandWidth:100,
          expandFixed:false,
          align:'center',
          menuFixed:false,
          menuAlign:'center',
          column:[
            {
              label:'姓名',
              prop:'name'
            }, {
              width:500,
              label:'性别',
              prop:'sex'
            }
          ]
        },
      };
    }
}
</script>
```

[表格高级用法](https://v2.avuejs.com/crud/crud-ajax/) [大表哥(宇宙最强表格)](https://v2.avuejs.com/crud/crud-bigcousin/)

您正在浏览基于 Vue 2.x 的 Avue 文档；**[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号