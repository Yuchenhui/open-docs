操作栏配置
=====

操作栏隐藏  
`menu`属性接受一个`Boolean`的属性达到隐藏操作栏的效果，默认为`false`

```vue
<avue-crud :data="data" :option="option1"></avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' }
        ],
        option1:{
          menu:false,
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    }
}
</script>
```

操作栏对齐方式  
`menuWidth`属性设置操作栏宽度, `menuTitle`属性设置操作栏目的文字, `menuAlign`属性设置对齐方式, `menuHeaderAlign`属性设置表头对齐方式

```vue
<avue-crud :data="data" :option="option1"></avue-crud>
<script>
export default {
  data () {
    return {
      data:[
        { name: '张三', sex: '男' },
        { name: '李四', sex: '女' }
      ],
      option1: {
        menuTitle: '其它',
        menuWidth: 250,
        menuAlign: 'left',
        menuHeaderAlign: 'left',
        column:[
          { label: '姓名', prop: 'name' },
          { label: '性别', prop: 'sex' }
        ]
      },
    };
  }
}
</script>
```

操作栏自适应  
通过`js`计算元素宽度，动态给`menuWidth`赋值，实现动态宽度

```vue
<avue-crud :data="data" :option="option">
  <template #menu="{size}">
    <el-button v-for="(item,index) in 5" :key="index" :size="size" type="text">操作{{index+1}}</el-button>
  </template>
</avue-crud>
<script>
export default {
  data () {
    return {
      data:[
        { name: '张三', sex: '男' },
        { name: '李四', sex: '女' }
      ],
      option: {
        menuWidth: 0,
        column:[
          { label: '姓名', prop: 'name' },
          { label: '性别', prop: 'sex' }
        ]
      },
    };
  },
  mounted () {
    this.setMenuWidth()
  },
  methods: {
    setMenuWidth () {
      setTimeout(() => {
        let width = 0;
        let list = document.querySelectorAll('.avue-crud__menu');
        list.forEach(ele => {
          let childList = ele.children
          let allWidth = 0;
          for (let i = 0; i < childList.length; i++) {
            const child = childList[i]
            allWidth += child.offsetWidth + 18
          }
          if (allWidth >= width) width = allWidth
        })
        this.option.menuWidth = width
      })
    }
  }
}
</script>
```

操作栏样式  
`menuClassName`属性和`menuLabelClassName`属性配置操作栏列的单元格和表头样式名称

```vue
<avue-crud :data="data" :option="option1"></avue-crud>
<script>
export default {
  data () {
    return {
      data:[
        { name: '张三', sex: '男' },
        { name: '李四', sex: '女' }
      ],
      option1: {
        menuClassName: 'menuClassName',
        menuLabelClassName: 'menuLabelClassName',
        column:[
          { label: '姓名', prop: 'name' },
          { label: '性别', prop: 'sex' }
        ]
      },
    };
  }
}
</script>
```

自定义操作栏头部  
`menuHeader`插槽为操作栏头部自定义

```vue
<avue-crud :data="data" :option="option">
  <template #menuHeader="{}">
      <el-tag @click="tip()">操作</el-tag>
    </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' }
        ],
        option:{
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    },
    methods: {
      tip(){
        this.$message.success('自定义头部按钮');
      }
    }
}
</script>
```

自定义操作栏  
`menu`为操作栏自定义

```vue
<avue-crud :data="data" :option="option">
  <template slot-scope="{type,size,row,index}" slot="menu">
     <el-button icon="el-icon-check" :size="size" :type="type" @click="tip(row,index)">自定义菜单按钮</el-button>
  </template>
  <template slot-scope="{type,size,row,index}" slot="menuBefore">
      <el-button @click="tip(row,index)" icon="el-icon-check" :type="type" :size="size">自定义前菜单</el-button>
    </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' }
        ],
        option:{
          menuWidth:380,
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    },
    methods: {
      tip(row){
        this.$message.success('自定义按钮'+ JSON.stringify(row));
      }
    }
}
</script>
```

查看按钮  
`viewBtn`配置为`true`即可

```vue
<avue-crud ref="crud" :option="option" :data="data"></avue-crud>
<script>
export default {
  data(){
    return {
       data:[
         { name:'张三', age:12, address:'码云的地址' },
         { name:'李四', age:13, address:'码云的地址' }
       ],
       option:{
          viewBtn:true,
          editBtn:false,
          delBtn:false,
          column: [
            { label: '姓名', prop: 'name' },
            { label: '年龄', prop: 'age' },
            { label:'地址', span:24, prop:'address', type:'textarea' }
          ]
       }
    }
  }
}
</script>
```

复制按钮  
设置`copyBtn`为`true`时激活行复制功能，复制的数据会去除`rowKey`配置的主键

```vue
{{form}}
<avue-crud :data="data" :option="option" v-model="form"></avue-crud>

<script>
export default {
    data() {
      return {
        form:{},
        data:[
          { ids:1, name:'张三', sex:'男' },
          { ids:2, name:'李四', sex:'女' }
        ],
        option:{
          rowKey:'ids',
          copyBtn:true,
          delBtn:false,
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    }
}
</script>
```

打印按钮  
`printBtn`设置为`true`即可开启打印功能

```vue
<avue-crud :option="option" :data="data"></avue-crud>
<script>
export default {
  data(){
    return {
       data:[
          { text1:'内容1-1', text2:'内容1-2' },
          { text1:'内容2-1', text2:'内容2-2' }
       ],
       option:{
          menu:false,
          printBtn:true,
          column: [
            { label: '列内容1', prop: 'text1' },
            { label: '列内容2', prop: 'text2' }
          ]
       }
    }
  }
}
</script>
```

导出按钮  
导入需要的包（一定要放到index.html中的head标签里）:

```html
<script src="https://cdn.staticfile.net/FileSaver.js/2014-11-29/FileSaver.min.js"></script>
<script src="https://cdn.staticfile.net/xlsx/0.18.2/xlsx.full.min.js"></script>
```

`excelBtn`设置为`true`即可开启表格导出功能

```vue
<avue-crud :option="option" :data="data"></avue-crud>
<script>
export default {
  data(){
    return {
       data:[
          { text1:'内容1-1', text2:'内容1-2' },
          { text1:'内容2-1', text2:'内容2-2' }
       ],
       option:{
          menu:false,
          excelBtn:true,
          column: [
            { label: '列内容1', prop: 'text1' },
            { label: '列内容2', prop: 'text2' }
          ]
       }
    }
  }
}
</script>
```

筛选按钮  
`filterBtn`默认为`true`，可以自定义过滤条件，根据`filter`函数回调

```vue
<avue-crud :option="option" :data="data" @filter="filterChange"></avue-crud>
<script>
export default {
  data(){
    return {
       data:[
          { text1:'内容1-1', text2:'内容1-2' },
          { text1:'内容2-1', text2:'内容2-2' }
       ],
       option:{
          filterBtn:true,
          align:'center',
          column: [
            { label: '列内容1', prop: 'text1' },
            { label: '列内容2', prop: 'text2' }
          ]
       }
    }
  },
  methods:{
    filterChange(result) {
      this.$message.success('过滤器' + JSON.stringify(result))
    },
  }
}
</script>
```

合并菜单  
配置`menuType`为`menu`表格的操作栏目菜单合并，`menuBtn`插槽为自定义卡槽

```vue
<avue-crud :data="data" :option="option" >
  <template slot-scope="{row}" slot="menuBtnBefore">
       <el-dropdown-item @click.native="tip(row)">自定义按钮</el-dropdown-item>
    </template>
    <template slot-scope="{row}" slot="menuBtn">
       <el-dropdown-item divided @click.native="tip(row)">自定义按钮</el-dropdown-item>
    </template>
</avue-crud>

<script>
export default {
 data() {
      return {
        data:[
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' },
          { name:'王五', sex:'女' },
          { name:'赵六', sex:'男' }
        ],
        option:{
          menuType:'menu',
          menuBtnTitle:'自定义名称',
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        }
      }
    },
    methods: {
      tip(row){
        this.$message.success('自定义按钮'+ JSON.stringify(row));
      }
    }
  }
</script>
```

图标菜单  
配置`menuType`为`icon`时表格操作栏为图标按钮

```vue
<avue-crud :data="data" :option="option">
  <template slot-scope="{row}" slot="menu">
     <el-button size="small" @click="tip(row)" icon="el-icon-share"></el-button>
  </template>
</avue-crud>

<script>
export default {
 data() {
      return {
        data:[
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' },
          { name:'王五', sex:'女' },
          { name:'赵六', sex:'男' }
        ],
        option:{
          menuType:'icon',
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        }
      }
    },
    methods: {
      tip(row){
        this.$message.success('自定义按钮'+ JSON.stringify(row));
      }
    }
  }
</script>
```

[数据字典](https://v2.avuejs.com/crud/crud-dic/) [增删改查方法](https://v2.avuejs.com/crud/crud-fun/)  
您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本  
关注Avue Cloud公众号