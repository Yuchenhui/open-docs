DataOperatext 数据展示
==================
... 2021-7-29 Less than 1 minute

* * *

[#](https://v2.avuejs.com/data/data7/#dataoperatext-%E6%95%B0%E6%8D%AE%E5%B1%95%E7%A4%BA)
 DataOperatext 数据展示
=============================================================================================================

Tips

1.0.4+

```vue
<avue-data-operatext :option="option"></avue-data-operatext>
<script>
export default {
  data(){
    return {
      option: {
        span: 8,
        data: [
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: 'smallwei',
            subtitle: 'avue部门-前端研发工程师',
            img: 'https://avatar.gitee.com/uploads/61/632261_smallweigit.jpg!avatar100?1518660401',
            color: '#00a7d0',
            list: [
              { label: '点赞', value: '3,200' },
              { label: '关注', value: '13,000' },
              { label: '项目', value: '13,000' }
            ]
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: 'smallwei',
            subtitle: 'avue部门-前端研发工程师',
            img: 'https://avatar.gitee.com/uploads/61/632261_smallweigit.jpg!avatar100?1518660401',
            color: '#f39c12',
            list: [
              { label: '点赞', value: '3,200' },
              { label: '关注', value: '13,000' },
              { label: '项目', value: '13,000' }
            ]
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: 'smallwei',
            subtitle: 'avue部门-前端研发工程师',
            img: 'https://avatar.gitee.com/uploads/61/632261_smallweigit.jpg!avatar100?1518660401',
            colorImg: 'http://img.sccnn.com/bimg/337/15595.jpg',
            list: [
              { label: '点赞', value: '3,200' },
              { label: '关注', value: '13,000' },
              { label: '项目', value: '13,000' }
            ]
          }
        ]
      },
    }
  }
}
</script>
```

[DataIcons 数据展示](https://v2.avuejs.com/data/data6/) [DataProgress 数据展示](https://v2.avuejs.com/data/data8/)

Install Cancel

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号