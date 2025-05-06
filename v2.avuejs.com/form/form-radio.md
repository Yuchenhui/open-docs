Radio单选框
========

基础用法
--------------------------------------------------------------------------------------
> 由于选项默认可见，不宜过多，若选项过多，建议使用 Select 选择器。

通过将`type`属性的值指定为`radio`,同时配置`dicData`为字典值

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: '多选',
          prop: 'radio',
          type: 'radio',
          dicData:[
            {label:'男', value:0},
            {label:'女', value:1},
            {label:'未知', value:''}
          ]
        }]
      }
    }
  }
}
</script>
```

网络字典
--------------------------------------------------------------------------------------
> 更多用法参考[表单数据字典](https://v2.avuejs.com/form/form-dic)

配置`dicUrl`指定后台接口的地址

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data(){
    return {
      option:{
        column: [{
          label:'单选框',
          prop:'radio',
          type:'radio',
          props: {
            label: 'name',
            value: 'code'
          },
          dicUrl: 'https://cli.avuejs.com/api/area/getProvince'
        }]
      }
    }
  }
}
</script>
```

默认值
------------------------------------------------------------------------------
`value`属性可以提供一个初始化的默认值

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'单选框',
          prop:'radio',
          type:'radio',
          dicData:[
            {label:'男', value:0},
            {label:'女', value:1},
            {label:'未知', value:''}
          ],
          value:0
        }]
      }
    }
  }
}
</script>
```

禁用状态
--------------------------------------------------------------------------------------
通过`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'单选框',
          prop:'radio',
          type:'radio',
          dicData:[
            {label:'男', value:0},
            {label:'女', value:1},
            {label:'未知', value:''}
          ],
          disabled:true
        }]
      }
    }
  }
}
</script>
```

禁用选项
--------------------------------------------------------------------------------------
返回的字典中数据配置`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'单选框',
          prop:'radio',
          type:'radio',
          dicData:[
            {label:'男', value:0},
            {label:'女', value:1, disabled:true},
            {label:'未知', value:''}
          ]
        }]
      }
    }
  }
}
</script>
```

按钮样式
--------------------------------------------------------------------------------------
配置`button`为`true`

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: '实心多选',
          prop: 'radio',
          type: 'radio',
          button:true,
          dicData:[
            {label:'男', value:0},
            {label:'女', value:1},
            {label:'未知', value:''}
          ]
        }]
      }
    }
  }
}
</script>
```

空心样式
--------------------------------------------------------------------------------------
配置`border`为`true`

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data() {
    return {
      option: {
        column: [{
          label: '空心多选',
          prop: 'radio',
          type: 'radio',
          border:true,
          dicData:[
            {label:'男', value:0},
            {label:'女', value:1},
            {label:'未知', value:''}
          ]
        }]
      }
    }
  }
}
</script>
```

[Checkbox多选框](https://v2.avuejs.com/form/form-checkbox/) [Date日期](https://v2.avuejs.com/form/form-date/)