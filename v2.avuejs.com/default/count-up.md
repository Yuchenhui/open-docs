CountUp数字动画
===========

数字动画效果

Tips

1.0.10+

```html
<div style="font-size:43px;font-weight:500;color:red;">
  <p><avue-count-up :end="15033.2"></avue-count-up></p>
  <p><avue-count-up :end="1233.2" :start="1000"></avue-count-up></p>
</div>
<script>
export default {
  
}
</script>
```

Variables
---------

| 参数      | 说明           | 类型     | 可选值 | 默认值 |
| --------- | -------------- | -------- | ------ | ------ |
| start     | 开始时的数字   | Number   | -      | 0      |
| end       | 结束时的数字   | Number   | -      | -      |
| decimals  | 是否支持小数   | Number   | -      | 0      |
| duration  | 动画速度       | Number   | -      | 2      |
| options   | CountUp.js其他配置 | Object | -      | -      |
| callback  | 开始时候的回调 | Function | -      | -      |

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本 关注Avue Cloud公众号