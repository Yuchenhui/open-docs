DataDisplay 数据展示
================

```vue
<avue-data-display :option="option"></avue-data-display>
<script>
  export default {
    data() {
      return {
        option: {
          span: 6,
          data: [
            {
              click: function (item) {
                alert(JSON.stringify(item));
              },
              count: 100,
              decimals: 2,
              title: "日活跃数",
              href: "https://avuejs.com",
              target: "_blank",
            },
            {
              click: function (item) {
                alert(JSON.stringify(item));
              },
              count: "3,000",
              title: "月活跃数",
              color: "red",
              fontColor: "#000",
              href: "https://avuejs.com",
              target: "_blank",
            },
            {
              click: function (item) {
                alert(JSON.stringify(item));
              },
              count: "20,000",
              title: "年活跃数",
              href: "https://avuejs.com",
              target: "_blank",
            },
            {
              click: function (item) {
                alert(JSON.stringify(item));
              },
              count: "40,000",
              title: "周活跃数",
              href: "https://avuejs.com",
              target: "_blank",
            },
          ],
        },
      };
    },
  };
</script>
```

Attributes
----------

| 参数      | 说明      | 类型     | 可选值         | 默认值 |
| --------- | --------- | -------- | -------------- | ------ |
| animation | 是否动画  | Boolean  | false/true     | true   |
| decimals  | 小数点位数 | Number   | —              | 0      |
| span      | 栅格数    | String   | —              | 8      |
| data      | 数据      | Array    | —              | -      |

[DataCardtext 数据展示](https://v2.avuejs.com/data/data4/) [DataIcons 数据展示](https://v2.avuejs.com/data/data6/)