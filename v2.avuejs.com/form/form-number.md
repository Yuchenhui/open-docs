Number数字输入框
===========

基础用法
---------------------------------------------------------------------------------------
通过将`type`属性的值指定为`number`

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            type:'number'
         }
        ]
      }
    }
  }
}
</script>
```

默认值
-----------------------------------------------------------------------------
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
            label:'数字输入框',
            prop:'num',
            type:'number',
            value:2
         }
        ]
      }
    }
  }
}
</script>
```

禁用状态
---------------------------------------------------------------------------------------
`disabled`属性接受一个Boolean，设置为`true`即可禁用整个组件

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            type:'number',
            disabled:true
         }
        ]
      }
    }
  }
}
</script>
```

最大值最小值
-----------------------------------------------------------------------------------------------------------
如果你只需要控制数值在某一范围内，可以设置`min`属性和`max`属性，不设置`min`和`max`时，最小值为 `0`。

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            min:1,
            max:2,
            type:'number'
         }
        ]
      }
    }
  }
}
</script>
```

步数
-------------------------------------------------------------------
设置`step`属性可以控制步长，接受一个`Number`。

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            type:'number',
            step:2,
         }
        ]
      }
    }
  }
}
</script>
```

严格步数
---------------------------------------------------------------------------------------
`stepStrictly`属性接受一个`Boolean`。如果这个属性被设置为`true`，则只能输入步数的倍数。

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            type:'number',
            step:2,
            stepStrictly:true,
         }
        ]
      }
    }
  }
}
</script>
```

隐藏控制器
-------------------------------------------------------------------------------------------------
设置`controls`属性是否使用控制按钮。

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            type:'number',
            controls:false,
         }
        ]
      }
    }
  }
}
</script>
```

尺寸
-------------------------------------------------------------------
可通过`size`属性指定输入框的尺寸，默认为`small`，还提供了`large`,`small`和`mini`三种尺寸。

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'input',
            type:'number',
            size:'large',
         },
         {
            label:'数字输入框',
            prop:'input1',
            type:'number'
         },
         {
            label:'数字输入框',
            prop:'input2',
            type:'number',
            size:'mini'
         }
        ]
      }
    }
  }
}
</script>
```

精度
-------------------------------------------------------------------
设置`precision`属性可以控制数值精度，接收一个`Number`。

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            type:'number',
            precision:2,
         }
        ]
      }
    }
  }
}
</script>
```

按钮位置
---------------------------------------------------------------------------------------
设置 `controlsPosition`属性可以控制按钮位置。

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'数字输入框',
            prop:'num',
            controlsPosition:'',
            type:'number'
         }
        ]
      }
    }
  }
}
</script>
```

[Input输入框](https://v2.avuejs.com/form/form-input/) [Select选择框](https://v2.avuejs.com/form/form-select/)