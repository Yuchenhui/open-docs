Draggable 拖拽
============

* 用该组件包裹后可以变成拖拽组件,采用相对于父类绝对定位
* 用键盘的上下左右也可以控制移动

Tips

2.5.3+

```html
<div style="position:relative;height:400px;" @mousedown="handleMouseDown">
  <div class="avue-grid"></div>
  <avue-draggable :width="obj.width" :height="obj.height" :left="obj.left" :top="obj.top" id="draggable" ref="draggable" @focus="handleFocus" @blur="handleBlur">
    <div style="width:200px;height:200px;background:red"></div>
  </avue-draggable>
  <avue-draggable :width="obj1.width" :height="obj1.height" :left="obj1.left" :top="obj1.top" id="draggable1" ref="draggable1" @focus="handleFocus" @blur="handleBlur">
    <div style="width:200px;height:200px;background:green"></div>
  </avue-draggable>
  <avue-draggable lock :width="obj2.width" :height="obj2.height" :left="obj2.left" :top="obj2.top" id="draggable2" ref="draggable2" @focus="handleFocus" @blur="handleBlur">
    <div style="width:200px;height:200px;background:yellow"></div>
  </avue-draggable>
</div>

<script>
export default {
  data() {
    return {
      obj: {
        width: 100,
        height: 100,
        left: 100,
        top: 100
      },
      obj1: {
        width: 200,
        height: 200,
        left: 300,
        top: 200
      },
      obj2: {
        width: 100,
        height: 100,
        left: 500,
        top: 200
      }
    }
  },
  methods: {
    handleMouseDown() {
      // 调用内部方法取消选中，false取消，true激活
      this.$refs.draggable1.setActive(false);
    },
    // 获取焦点
    handleFocus({ index, left, top, width, height }) {
      console.log(index, left, top, width, height);
    },
    // 失去焦点
    handleBlur({ index, left, top, width, height }) {
      console.log(index, left, top, width, height);
    }
  }
}
</script>
```

Variables
---------

| 参数      | 说明       | 类型 | 可选值 | 默认值 |
| --------- | ---------- | ---- | ------ | ------ |
| disabled  | 是否禁止拖动 | —    | false  |        |
| width     | 元素的宽度 | —    | —      |        |
| height    | 元素的高度 | —    | —      |        |
| top       | 元素的x位置 | —    | 0      |        |
| left      | 元素的y位置 | —    | 0      |        |
| z-index   | 图层的序号 | -    | 1      |        |

Events
------

| 事件名 | 说明       | 参数 |
| ------ | ---------- | ---- |
| focus  | 聚焦时回调 | -    |
| blur   | 失去焦点回调 | -    |
| move   | 移动中回调 | -    |
| out    | 鼠标移出回调 | -    |
| over   | 鼠标移入回调 | -    |

Methods
-------

| 方法名   | 说明             | 参数 |
| -------- | ---------------- | ---- |
| setActive | 改变选中不选中的状态 | -    |

[Card 卡片](https://v2.avuejs.com/default/card/) [ImagePreview 图片预览](https://v2.avuejs.com/default/image-preview/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/) 查看 Vue 3.x 的升级版本**

关注Avue Cloud公众号