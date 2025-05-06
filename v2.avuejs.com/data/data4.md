DataCardtext 数据展示
=================

2021-7-29 Less than 1 minute

[#](https://v2.avuejs.com/data/data4/#datacardtext-%E6%95%B0%E6%8D%AE%E5%B1%95%E7%A4%BA)
DataCardtext 数据展示

Tips

1.0.2+

```vue
<avue-data-cardtext :option="option"></avue-data-cardtext>
<script>
export default {
  data(){
    return {
      option: {
        span: 6,
        data: [
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '香菜',
            color: 'yellow',
            icon: 'el-icon-mobile-phone',
            content: '殷其雷，天阴霾，雨零耶，盼君留。 殷其雷，纵不零，卿若留，吾将从。',
            href: "http://www.baidu.com",
            target: '_blank',
            name: '文件上传',
            date: '1天前'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '钉宫',
            icon: 'el-icon-bell',
            color: 'green',
            content: '殷其雷，天阴霾，雨零耶，盼君留。 殷其雷，纵不零，卿若留，吾将从。',
            href: "http://www.baidu.com",
            name: '流加载',
            date: '1天前'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '亚丝娜',
            icon: 'el-icon-service',
            color: '#3fa1ff',
            content: '殷其雷，天阴霾，雨零耶，盼君留。 殷其雷，纵不零，卿若留，吾将从。',
            href: "http://www.baidu.com",
            name: '表单',
            date: '1天前'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '狂三',
            icon: 'el-icon-time',
            color: 'red',
            content: '殷其雷，天阴霾，雨零耶，盼君留。 殷其雷，纵不零，卿若留，吾将从。',
            href: "http://www.baidu.com",
            name: '文件上传',
            date: '1天前'
          }
        ]
      },
    }
  }
}
</script>
```

[DataCard 数据展示](https://v2.avuejs.com/data/data3/) [DataDisplay 数据展示](https://v2.avuejs.com/data/data5/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号