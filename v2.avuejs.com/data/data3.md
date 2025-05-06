DataCard 数据展示
=============

[#](https://v2.avuejs.com/data/data3/#datacard-%E6%95%B0%E6%8D%AE%E5%B1%95%E7%A4%BA) DataCard 数据展示
===================================================================================================

```vue
<avue-data-card :option="option"></avue-data-card>
<script>
export default {
  data(){
    return {
      option: {
        span:8,
        data: [
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            name: '小马',
            src: '/images/card-1.jpg',
            text: 'xxxxxxxx',
            href:'https://avuejs.com',
            target:'_blank'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            name: '网易掌门人',
            src: '/images/card-3.jpg',
            text: 'xxxxxx',
            href:'https://avuejs.com',
            target:'_blank'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            name: '桐谷和人',
            src: '/images/card-4.jpg',
            text: 'xxxxx',
            href:'https://avuejs.com',
            target:'_blank'
          }
        ]
      },
    }
  }
}
</script>
```

[DataBox 数据展示](https://v2.avuejs.com/data/data2/) [DataCardtext 数据展示](https://v2.avuejs.com/data/data4/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号