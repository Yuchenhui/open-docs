DataProgress 数据展示
=================

```vue
<avue-data-progress :option="option"></avue-data-progress>
<script>
export default {
  data(){
    return {
      option: {
        span:6,
        data: [
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '转化率（日同比 28%）',
            color: 'rgb(178, 159, 255)',
            count: 32,
            href:'https://avuejs.com',
            target:'_blank'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '签到率（日同比 11%）',
            color:'rgb(230, 71, 88)',
            count: 32,
            href:'https://avuejs.com',
            target:'_blank'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: 'CPU使用率',
            color:'rgb(27, 201, 142)',
            count: 56,
            href:'https://avuejs.com',
            target:'_blank'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '使用人数',
            color:'red',
            count: 56,
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

Attributes
-------------------------------------------------------------

| 参数  | 说明       | 类型    | 可选值       | 默认值 |
|-------|------------|---------|--------------|--------|
| animation | 是否动画 | Boolean | false/true   | true   |
| decimals  | 小数点位数 | Number  | —            | 0      |
| span      | 栅格数     | String  | —            | 8      |
| data      | 数据       | Array   | —            | -      |

[DataOperatext 数据展示](https://v2.avuejs.com/data/data7/) [DataRotate 数据展示](https://v2.avuejs.com/data/data9/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本 关注Avue Cloud公众号