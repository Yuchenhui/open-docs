Slider滑块
========

基础用法
---------------------------------------------------------------------------------------

通过将`type`属性的值指定为`slider`

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "普通滑块",
          prop: "slider",
          type: 'slider',
        }, {
          label: "初始化值",
          prop: "slider",
          type: 'slider',
          value: 2
        }, {
          label: "隐藏提示",
          prop: "slider",
          type: 'slider',
          showTooltip: false
        }, {
          label: "格式化值",
          prop: "slider",
          type: 'slider',
          formatTooltip: function(val) {
            return '格式化的值' + val;
          }
        }, {
          label: "禁用",
          prop: "slider",
          type: 'slider',
          disabled: true
        }]
      }
    }
  }
}
</script>
```

离散值
-----------------------------------------------------------------------------

> 选项可以是离散的

改变`step`的值可以改变步长，通过设置`showStops`属性可以显示间断点

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "滑块",
          prop: "slider",
          type: 'slider',
          step: 10,
          showStops: true,
        }, {
          label: "滑块",
          prop: "slider",
          type: 'slider',
          step: 10
        }]
      }
    }
  }
}
</script>
```

带有输入框
-------------------------------------------------------------------------------------------------

> 通过输入框设置精确数值

设置`showInput`属性会在右侧显示一个输入框

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "滑块",
          prop: "slider",
          type: 'slider',
          showInput: true
        }]
      }
    }
  }
}
</script>
```

范围选择
---------------------------------------------------------------------------------------

> 支持选择某一数值范围

设置`range`即可开启范围选择，此时绑定值是一个数组，其元素分别为最小边界值和最大边界值

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "滑块",
          prop: "slider",
          type: 'slider',
          showStops: true,
          max: 10,
          range: true,
          value: [4, 8]
        }]
      }
    }
  }
}
</script>
```

竖向模式
---------------------------------------------------------------------------------------

设置`vertical`可使 Slider 变成竖向模式，此时必须设置高度`height`属性

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "滑块",
          prop: "slider",
          type: 'slider',
          vertical: true,
          height: 200
        }]
      }
    }
  }
}
</script>
```

展示标记
---------------------------------------------------------------------------------------

设置`marks`属性可以展示标记

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "滑块",
          prop: "slider",
          type: 'slider',
          range: true,
          value: [30, 60],
          marks: {
            0: '0°C',
            8: '8°C',
            37: '37°C',
            50: {
              style: {
                color: '#1989FA'
              },
              label: this.$createElement('strong', '50%')
            }
          }
        }]
      }
    }
  }
}
</script>
```