Input输入框
========

基础用法
--------
当`type`为`input`时可以不写,默认为`input`

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'输入框',
            prop:'input',
            type:'input'
         },
         {
            label:'输入框',
            prop:'input1'
         }
        ]
      }
    }
  }
}
</script>
```

默认值
------
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
            label:'输入框',
            prop:'input',
            value:'默认值'
         }
        ]
      }
    }
  }
}
</script>
```

禁用状态
--------
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
            label:'输入框',
            prop:'input',
            disabled:true
         }
        ]
      }
    }
  }
}
</script>
```

可清空
-------
使用`clearable`属性即可得到一个可清空的输入框,默认为`true`

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'输入框',
            prop:'input',
            clearable:false
         }
        ]
      }
    }
  }
}
</script>
```

密码框
------
> 用于密码，通过将 type 属性的值指定为 password  
使用`showPassword`属性即可得到一个可切换显示隐藏的密码框

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'密码框',
            prop:'input',
            type:'password',
            showPassword:true
         }
        ]
      }
    }
  }
}
</script>
```

文本域
------
> 用于文本域，通过将 type 属性的值指定为 textarea,文本域高度可通过 rows 属性控制  
通过设置`maxRows`和`minRows`，指定最小行数和最大行数,使得文本域的高度能够根据文本内容自动进行调整

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'文本域',
            prop:'input',
            type:'textarea',
            minRows:3,
            maxRows:5
         },
         {
            label:'文本域',
            prop:'input1',
            type:'textarea',
            rows:5
         }
        ]
      }
    }
  }
}
</script>
```

尺寸
-----
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
            label:'输入框',
            prop:'input',
            size:'large',
         },
         {
            label:'输入框',
            prop:'input1'
         },
         {
            label:'输入框',
            prop:'input2',
            size:'mini'
         }
        ]
      }
    }
  }
}
</script>
```

复合型输入框
----------
> 带有图标标记输入类型  
可以通过 `prefixIcon` 和 `suffixIcon`以及`prepend`和`append`属性在 `input` 组件首部和尾部增加显示图标

```vue
<avue-form :option="option" v-model="form"></avue-form>

<script>
export default{
  data() {
    return {
      form: {},
      option: {
        column: [
         {
            label:'输入框',
            prop:'input',
            appendClick: () => {
              ElMessage.success('appendClick')
            },
            prependClick: () => {
              ElMessage.success('prependClick')
            },
            prepend:'HTTP',
            append:'COM'
         },
         {
            label:'输入框',
            prop:'input1',
            suffixIcon:"el-icon-date",
            prefixIcon:"el-icon-search"
         }
        ]
      }
    }
  }
}
</script>
```

输入长度限制
-----------
`maxlength` 和 `minlength` 是原生属性，用来限制输入框的字符长度，其中字符长度是用 `Javascript` 的字符串长度统计的。在使用 `maxlength` 属性限制最大输入长度的同时，可通过设置 `showWordLimit` 属性来展示字数统计。

```vue
<avue-form :option="option" v-model="form"></avue-form>

<script>
export default{
  data() {
    return {
      form: {},
      option: {
        column: [
         {
            label:'单文本框',
            prop:'input',
            maxlength:10,
            showWordLimit:true
         }, {
            label:'多文本框',
            prop:'textarea',
            type:'textarea',
            maxlength:20,
            minRows:3,
            maxRows:5,
            span:24,
            showWordLimit:true
         }
        ]
      }
    }
  }
}
</script>
```

[Form属性文档](https://v2.avuejs.com/form/form-doc/) [Number数字输入框](https://v2.avuejs.com/form/form-number/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号