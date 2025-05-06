DataPrice 数据展示
==============

Tips

2.0.5+

    <avue-data-price :option="option"></avue-data-price>
    <script>
    export default {
      data() {
         return {
           option: {
             span: 6,
             data: [
               {
                 title: '日套餐',
                 price: 20,
                 append: '1 / 天',
                 click: function () {
                   alert('弹窗');
                 },
                 list: ['1天的使用时间', '支持pc客户端', '支持vue的全部体系', '一个神奇的框架']
               }, {
                 title: '周套餐',
                 price: 30,
                 append: '7 / 天',
                 click: function () {
                   alert('弹窗');
                 },
                 list: ['1天的使用时间', '支持pc客户端', '支持vue的全部体系', '一个神奇的框架']
               }, {
                 title: '月套餐',
                 price: 40,
                 append: '30 / 天',
                 click: function () {
                   alert('弹窗');
                 },
                 list: ['1天的使用时间', '支持pc客户端', '支持vue的全部体系', '一个神奇的框架']
               }, {
                 title: '年套餐',
                 price: 50,
                 append: '360 / 天',
                 click: function () {
                   alert('弹窗');
                 },
                 list: ['1天的使用时间', '支持pc客户端', '支持vue的全部体系', '一个神奇的框架']
               }
             ]
           }
         }
       },
    }
    </script>
    
Attributes
--------------------------------------------------------------

| 参数  | 说明       | 类型    | 可选值      | 默认值 |
| ---   | ---        | ---     | ---         | ---    |
| animation | 是否动画 | Boolean | false/true  | true   |
| decimals  | 小数点位数 | Number | —           | 0      |
| span      | 栅格数    | String  | —           | 8      |
| data      | 数据      | Array   | —           | -      |

[DataPanel 数据展示](https://v2.avuejs.com/data/data11/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号