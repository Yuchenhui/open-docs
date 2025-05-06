Time时间
======

[#](https://v2.avuejs.com/form/form-time/#time%E6%97%B6%E9%97%B4) Time时间
=========================================================================

[#](https://v2.avuejs.com/form/form-time/#%E5%9F%BA%E7%A1%80%E7%94%A8%E6%B3%95) 基础用法
-------------------------------------------------------------------------------------

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "时间",
          prop: "time",
          type: "time",
        }]
      },
    };
  }
}
</script>
```

[#](https://v2.avuejs.com/form/form-time/#%E4%B8%8B%E6%8B%89%E6%A1%86%E6%A0%B7%E5%BC%8F) 下拉框样式
-----------------------------------------------------------------------------------------------

```css
.popperClass .el-time-spinner__item {
  background-color: rgba(0,0,0,.2);
}
```

`popperClass`属性配置样式的`class`名字

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "时间",
          prop: "time",
          popperClass:'popperClass',
          type: "time",
        }]
      },
    };
  }
}
</script>
```

[#](https://v2.avuejs.com/form/form-time/#%E5%9B%BA%E5%AE%9A%E6%97%B6%E9%97%B4%E7%82%B9) 固定时间点
-----------------------------------------------------------------------------------------------

可设置`pickerOptions`中分别通过`start`、`end`和`step`指定可选的起始时间、结束时间和步长

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "时间",
          prop: "time",
          type: "time",
          pickerOptions: {
            start: '08:30',
            step: '00:15',
            end: '18:30'
          }
        }]
      },
    };
  }
}
</script>
```

[#](https://v2.avuejs.com/form/form-time/#%E6%A0%BC%E5%BC%8F%E5%8C%96) 格式化
---------------------------------------------------------------------------

使用`format`指定输入框的格式；使用`valueFormat`指定绑定值的格式。

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "时间",
          prop: "time",
          type: "time",
          format:'HH时mm分ss秒',
          valueFormat:'HH:mm:ss'
        }]
      },
    };
  }
}
</script>
```

[#](https://v2.avuejs.com/form/form-time/#%E6%97%B6%E9%97%B4%E8%8C%83%E5%9B%B4) 时间范围
-------------------------------------------------------------------------------------

```vue
<avue-form :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: "时间范围",
          prop: 'timerange',
          type: 'timerange',
          format: 'HH:mm:ss',
          valueFormat: 'HH:mm:ss',
          startPlaceholder: '时间开始范围自定义',
          endPlaceholder: '时间结束范围自定义',
        }]
      },
    };
  }
}
</script>
```

[#](https://v2.avuejs.com/form/form-time/#%E5%9B%BA%E5%AE%9A%E6%97%B6%E9%97%B4%E8%8C%83%E5%9B%B4) 固定时间范围
---------------------------------------------------------------------------------------------------------

> 若先选择开始时间，则结束时间内备选项的状态会随之改变

```vue
<avue-form v-model="form" :option="option"></avue-form>

<script>
export default {
  data() {
    return {
      form: {}
    };
  },
  computed: {
    option() {
      return {
        column: [{
          label: "开始时间",
          prop: 'start',
          type: 'time',
          format: 'HH:mm:ss',
          pickerOptions: {
            start: '08:30',
            step: '00:15',
            end: '18:30'
          }
        },{
          label: "结束时间",
          prop: 'end',
          type: 'time',
          format: 'HH:mm:ss',
          pickerOptions: {
            start: '08:30',
            step: '00:15',
            end: '18:30',
            minTime: this.form.start
          }
        }]
      }
    }
  }
}
</script>
```

[Date日期](https://v2.avuejs.com/form/form-date/) [Switch开关](https://v2.avuejs.com/form/form-switch/)