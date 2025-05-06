Color颜色选择器
==========

基础用法
--------------------------------------------------------------------------------------------

通过将`type`属性的值指定为`color`

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
          {
            label: '颜色选择器',
            prop: 'color',
            type: 'color'
          }
        ]
      }
    }
  }
}
</script>
```

默认值
----------------------------------------------------------------------------------

`value`属性可以提供一个初始化的默认值

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
          {
            label: '颜色选择器',
            prop: 'color',
            type: 'color',
            value: 'rgba(71, 46, 46, 1)'
          }
        ]
      }
    }
  }
}
</script>
```

禁用状态
--------------------------------------------------------------------------------------------

通过`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
          {
            label: '颜色选择器',
            prop: 'color',
            type: 'color',
            disabled: true
          }
        ]
      }
    }
  }
}
</script>
```

颜色格式
--------------------------------------------------------------------------------------------

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
          {
            label: '颜色选择器',
            prop: 'color',
            type: 'color',
            colorFormat: "hex",
            showAlpha: false
          }
        ]
      }
    }
  }
}
</script>
```

预定义颜色
------------------------------------------------------------------------------------------------------

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
          {
            label: '颜色选择器',
            prop: 'color',
            type: 'color',
            predefine: [
              '#ff4500',
              '#ff8c00',
              '#ffd700'
            ]
          }
        ]
      }
    }
  }
}
</script>
```

[Map坐标选择器](https://v2.avuejs.com/form/form-input-map/) [Rate评价](https://v2.avuejs.com/form/form-rate/)