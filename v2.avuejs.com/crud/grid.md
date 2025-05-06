卡片模式
====

Tips

2.12.0+

普通用法
-------------------------------------------------------------------------------------

`grid`配置为卡片模式,`gridBtn`和列表切换按钮，默认为`true`，在`v3.4.5`+新增 `grid-status-change`切换状态回调方法

```vue
<avue-crud :option="option" :data="data" @grid-status-change="gridStatusChange"></avue-crud>

<script>
let baseUrl = 'https://cli.avuejs.com/api/area'
export default{
  data() {
    return {
      data: [
        {
          name:'张三',
          sex:'男',
          age:18,
          province: '110000'
        }, {
          name:'李四',
          sex:'女',
          age:18,
          province: '130000'
        }
      ],
      option: {
        grid: true,
        column: [
          {
            label:'姓名',
            prop:'name',
          }, {
            label:'性别',
            prop:'sex',
            gridRow:true
          }, {
            label:'年龄',
            prop:'age',
          },{
            label:'省份',
            prop:'province',
            type:'select',
            props: {
                label: 'name',
                value: 'code'
            },
            dicUrl:`${baseUrl}/getProvince`
          }
        ]
      }
    }
  },
  methods: {
    gridStatusChange (val) {
      console.log('status', val)
    }
  }
}
</script>
```

配置
-----------------------------------------------------------------

一些配置用来改变布局和颜色

```vue
<avue-crud :option="option" :data="data" ></avue-crud>

<script>
let baseUrl = 'https://cli.avuejs.com/api/area'
export default{
  data() {
    return {
      data: [
        {
          name:'张三',
          sex:'男',
          age:18,
          province: '110000'
        }, {
          name:'李四',
          sex:'女',
          age:18,
          province: '130000'
        }
      ],
      option: {
        grid: true,
        gridSpan: 12,
        // gridBackground:'linear-gradient(to right, rgba(255,0,0,0.2), rgba(255,0,0,0.2))',
        gridBackgroundImage: '/images/grid.png',
        column: [
          {
            label:'姓名',
            prop:'name',
          }, {
            label:'性别',
            prop:'sex',
            gridRow:true
          }, {
            label:'年龄',
            prop:'age',
          },{
            label:'省份',
            prop:'province',
            type:'select',
            props: {
                label: 'name',
                value: 'code'
            },
            dicUrl:`${baseUrl}/getProvince`
          }
        ]
      }
    }
  }
}
</script>
```

方法
-----------------------------------------------------------------

gridBackground方法可以根据条件设置背景色

```vue
<avue-crud :option="option" :data="data" ></avue-crud>

<script>
export default{
  data() {
    return {
      data: [
        {
          name:'张三',
          sex:'男',
          age:18,
          province: '110000'
        }, {
          name:'李四',
          sex:'女',
          age:18,
          province: '130000'
        }
      ],
      option: {
        grid: true,
        gridSpan: 12,
        gridBackground: (row, index) => {
          if (index == 1) {
            return 'linear-gradient(to right, rgba(255,255,255,255.2), rgba(255,0,0,0.2))';
          } else {
            return 'linear-gradient(to right,  rgba(255,255,255,255.2), rgba(0,255,0,0.2))';
          }
        },
        column: [
          {
            label:'姓名',
            prop:'name',
          }, {
            label:'性别',
            prop:'sex',
            gridRow:true
          }, {
            label:'年龄',
            prop:'age',
          }
        ]
      }
    }
  }
}
</script>
```

自定义
---------------------------------------------------------------------------

```css
.imgbox {
  position: absolute;
  width: 80px;
  right: 20px;
  bottom: 60px;
}

.imgbox img {
  width: 100%;
}

.imgbox .avue-crud__grid__label {
  display: none;
}
```

利用插槽自定义

```vue
<avue-crud :option="option"
           :data="data">
  <template #img="{row}">
    <img :src="row.img"
         alt="">
  </template>
</avue-crud>

<script>
export default{
 data () {
    return {
      data: [
        {
          name: '张三',
          sex: '男',
          img: 'https://avuejs.com/images/logo.png',
          age: 18
        }, {
          name: '李四',
          sex: '女',
          img: 'https://avuejs.com/images/logo.png',
          age: 18
        }
      ],
      option: {
        grid: true,
        gridSpan: 12,
        gridBackgroundImage: '/images/grid.png',
        column: [
          {
            label: '姓名',
            prop: 'name',
            gridRow: true
          }, {
            label: '性别',
            prop: 'sex',
            gridRow: true
          }, {
            label: '年龄',
            prop: 'age',
            gridRow: true
          }, {
            label: '',
            display:false,
            className: "imgbox",
            prop: 'img'
          }
        ]
      }
    }
  }
}
</script>
```