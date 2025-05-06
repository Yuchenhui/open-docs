Cascader级联选择器
=============

基础用法
-----------------------------------------------------------------------------------------

通过将`type`属性的值指定为`cascader`,同时配置`dicData`为字典值,通过`expandTrigger`可以定义展开子级菜单的触发方式,默认为`hover`

```vue
<avue-form :option="option" ></avue-form>
<script>
const dicData=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        option: {
          column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dicData
          },{
            label: '级联',
            prop: 'cascader1',
            type: "cascader",
            expandTrigger:'click',
            dicData: dicData
          }]
      }
    }
  }
}
</script>
```

默认值
-------------------------------------------------------------------------------

`value`属性可以提供一个初始化的默认值

```vue
<avue-form :option="option" v-model="form"></avue-form>

<script>
const dicData=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default{
  data() {
    return {
      option: {
         column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dicData,
            value: [ "zhinan", "shejiyuanze", "yizhi" ]
         }]
      }
    }
  }
}
</script>
```

多选
---------------------------------------------------------------------

`multiple`为`true`在开启多选模式后，默认情况下会展示所有已选中的选项的Tag，你可以使用`tags`为`true`来折叠Tag

```vue
<avue-form v-model="form" :option="option"></avue-form>
<script>
const dic=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        form:{
          cascader: [ [ "zhinan", "shejiyuanze", "yizhi" ], [ "zhinan", "shejiyuanze", "fankui" ] ]
        },
        option: {
          column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dic,
            multiple: true
          },{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dic,
            tags:true,
            multiple: true
          }]
      }
    }
  }
}
</script>
```

禁用状态
-----------------------------------------------------------------------------------------

通过`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>

<script>
const dicData=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default{
  data() {
    return {
      option: {
        column: [
         {
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData:dicData,
            disabled:true
         }
        ]
      }
    }
  }
}
</script>
```

禁用选项
-----------------------------------------------------------------------------------------

返回的字典中数据配置`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>

<script>
const dicData=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      disabled:true,
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default{
  data() {
    return {
      option: {
        column: [
         {
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData:dicData
         }
        ]
      }
    }
  }
}
</script>
```

下拉框样式
---------------------------------------------------------------------------------------------------

```css
.popperClass .el-cascader-node{
  background-color: rgba(0,0,0,.2);
}
```

`popperClass`属性配置样式的`class`名字

```vue
<avue-form :option="option" v-model="form"></avue-form>

<script>
const dicData=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default{
  data() {
    return {
      option: {
         column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            popperClass:'popperClass',
            dicData: dicData
         }]
      }
    }
  }
}
</script>
```

网络字典
-----------------------------------------------------------------------------------------

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
            label: '级联框',
            prop: 'cascader',
            type: 'cascader',
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

仅显示最后一级
-----------------------------------------------------------------------------------------------------------------------

> 可以仅在输入框中显示选中项最后一级的标签，而不是选中项所在的完整路径。

属性`showAllLevels`定义了是否显示完整的路径，将其赋值为`false`则仅显示最后一级

```vue
<avue-form :option="option" ></avue-form>
<script>
const dicData=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        option: {
          column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dicData,
            showAllLevels:false
          }]
      }
    }
  }
}
</script>
```

选中单节点
---------------------------------------------------------------------------------------------------

> 在选中节点改变时，是否返回由该节点所在的各级菜单的值所组成的数组，若设置`false`，则只返回该节点的值

```vue
<avue-form  :option="option"></avue-form>
<script>
const dic=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        option: {
          column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            value:'yizhi',
            emitPath:false,
            dicData: dic
          }]
      }
    }
  }
}
</script>
```

任意一级
-----------------------------------------------------------------------------------------

> 在单选模式下，你只能选择叶子节点；而在多选模式下，勾选父节点真正选中的都是叶子节点。启用该功能后，可让父子节点取消关联，选择任意一级选项。

可通过`checkStrictly` 为`true` 来设置父子节点取消选中关联，从而达到选择任意一级选项的目的。

```vue
<avue-form  :option="option"></avue-form>
<script>
const dic=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        option: {
          column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dic,
            checkStrictly: true
          }]
      }
    }
  }
}
</script>
```

搜索
---------------------------------------------------------------------

> 可以快捷地搜索选项并选择。

将`filterable`赋值为true即可打开搜索功能，默认会匹配节点的label或所有父节点的label(由`showAllLevels`决定)中包含输入值的选项

```vue
<avue-form  :option="option"></avue-form>
<script>
const dic=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        option: {
          column: [ {
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dic,
            filterable: true
          }]
      }
    }
  }
}
</script>
```

自定义模版
---------------------------------------------------------------------------------------------------

配置`props`名称加`Type`卡槽开启即可自定义下拉框的内容

```vue
<avue-form  :option="option">
  <template slot="cascaderType" slot-scope="{node,data}">
    <span>{{ (data || {}).label }}</span>
    <span v-if="!node.isLeaf"> ({{((data || {}).children || []).length }}) </span>
  </template>
</avue-form>
<script>
const dic=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        option: {
          column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            dicData: dic
          }]
      }
    }
  }
}
</script>
```

懒加载
-------------------------------------------------------------------------------

```vue
<avue-form v-model="form" :option="option"></avue-form>
<script>
let baseUrl = 'https://cli.avuejs.com/api/area'
const dic=[{
  value: 'zhinan',
  label: '指南',
  children: [{
    value: 'shejiyuanze',
    label: '设计原则',
    children: [{
      value: 'yizhi',
      label: '一致'
    }, {
      value: 'fankui',
      label: '反馈'
    }]
  }]
}]
export default {
    data() {
      return {
        form:{
          cascader: ["110000", "110100", "110101"]
        },
        option: {
          column: [{
            label: '级联',
            prop: 'cascader',
            type: "cascader",
            props: {
              label: 'name',
              value: 'code'
            },
            lazy: true,
            lazyLoad(node, resolve) {
              let stop_level = 2;
              let level = node.level;
              let data = node.data || {}
              let code = data.code;
              let list = [];
              let callback = () => {
                resolve((list || []).map(ele => {
                  return Object.assign(ele, {
                    leaf: level >= stop_level
                  })
                }));
              }
              if (level == 0) {
                axios.get(`${baseUrl}/getProvince`).then(res => {
                  list = res.data;
                  callback()
                })
              }else if (level == 1) {
                axios.get(`${baseUrl}/getCity/${code}`).then(res => {
                  list = res.data;
                  callback()
                })
              } else if (level == 2) {
                axios.get(`${baseUrl}/getArea/${code}`).then(res => {
                  list = res.data;
                  callback()
                })
              }else{
                 callback()
              }
            }
          }]
      }
    }
  }
}
</script>
```

[Select选择框](https://v2.avuejs.com/form/form-select/) [Checkbox多选框](https://v2.avuejs.com/form/form-checkbox/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号