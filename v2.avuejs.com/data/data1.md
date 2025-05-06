DataTabs 数据展示
=============

<avue-data-tabs :option="option"></avue-data-tabs>
<script>
export default {
  data(){
    return {
      option: {
        data: [
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '分类统计',
            subtitle: '实时',
            count: 7993,
            allcount: 10222,
            text: '当前分类总记录数',
            color: 'rgb(27, 201, 142)',
            key: '类'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '附件统计',
            subtitle: '实时',
            count: 3112,
            allcount: 10222,
            text: '当前上传的附件数',
            color: 'rgb(230, 71, 88)',
            key: '附'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '文章统计',
            subtitle: '实时',
            count: 908,
            allcount: 10222,
            text: '评论次数',
            color: 'rgb(178, 159, 255)',
            key: '评'
          }
        ]
      }
    }
  }
}
</script>

Attributes
-------------------------------------------------------------

| 参数      | 说明       | 类型    | 可选值          | 默认值 |
| --------- | ---------- | ------- | --------------- | ------ |
| animation | 是否动画   | Boolean | false/true      | true   |
| decimals  | 小数点位数 | Number  | —               | 0      |
| span      | 栅格数     | String  | —               | 8      |
| data      | 数据       | Array   | —               | -      |

[DataPay 数据展示](https://v2.avuejs.com/data/data0/) [DataBox 数据展示](https://v2.avuejs.com/data/data2/)