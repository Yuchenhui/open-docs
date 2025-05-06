数据字典
====

数据字典
====================================================================================

Tips

更多字典详细用法参考[Form组件数据字典](https://v2.avuejs.com/form/form-dic.html)

```js
//使用字典需要引入axios
import axios from 'axios'
Vue.use(Avue,{axios})

//老版本需要使用如下
//main.js
window.axios = axios
```

字典使用
------------------------------------------------------------------------------------

本地字典配置`dicData`为一个`Array`数组，网络字典可以配置`dicUrl`字段，自动加载字典到对应的组件中，注意返回的字典中 value 类型和数据的类型必须要对应，比如都是字符串或者都是数字。配置`dicFlag`为`true`，打开表单的时候会重新请求字典

```vue
<avue-crud :data="data" :option="option" ></avue-crud>

<script>
let baseUrl = 'https://cli.avuejs.com/api/area'
export default {
    data() {
      return {
        data: [
          {
            province: '110000',
            cascader:[0,1],
          }, {
            province: '130000',
            cascader:[0,2],
          }
        ],
        option:{
          column:[
            {
              label:'本地字典',
              prop:'cascader',
              type:'cascader',
              dicData:[
                {
                  label:'一级',
                  value:0,
                  children:[
                    {
                      label:'一级1',
                      value:1,
                    },{
                      label:'一级2',
                      value:2,
                    }
                  ]
                }
              ],
            },
            {
              label:'网络字典',
              prop:'province',
              type:'select',
              props: {
                  label: 'name',
                  value: 'code'
              },
              dicFlag:true,
              dicUrl:`${baseUrl}/getProvince`
            }
          ]
        }
      }
    }
}
</script>
```

字典联动
------------------------------------------------------------------------------------

Tips

2.9.0+

`cascader`为需要联动的子选择框`prop`值，填写多个就会形成一对多的关系，表格加载联动数据需要调用内置方法`dicInit`

```vue
<avue-crud ref="crud" :data="data" :option="option" ></avue-crud>

<script>
let baseUrl = 'https://cli.avuejs.com/api/area'
export default {
    data() {
      return {
        data: [],
        option:{
          column:[
             {
              label:'姓名',
              prop:'name',
            }, {
              label:'性别',
              prop:'sex'
            },{
              label:'省份',
              prop:'province',
              type:'select',
              cascader: ['city'],
              cascaderIndex:1,
              props: {
                  label: 'name',
                  value: 'code'
              },
              dicUrl:`${baseUrl}/getProvince`
            },
            {
              width: 120,
              label: '城市',
              prop: 'city',
              type: 'select',
              cascader: ['area'],
              cascaderIndex:1,
              cell: true,
              props: {
                label: 'name',
                value: 'code'
              },
              dicUrl: `${baseUrl}/getCity/{{key}}`,
              rules: [
                {
                  required: true,
                  message: '请选择城市',
                  trigger: 'blur'
                }
              ]
            },
            {
              width: 120,
              label: '地区',
              prop: 'area',
              cell: true,
              props: {
                label: 'name',
                value: 'code'
              },
              type: 'select',
              dicUrl: `${baseUrl}/getArea/{{key}}`,
              rules: [
                {
                  required: true,
                  message: '请选择地区',
                  trigger: 'blur'
                }
              ]
            }
          ]
        }
      }
    },
    mounted(){
      this.data=[
        {
          name:'张三',
          sex:'男',
          province: '110000',
          city: '110100',
          area: '110101',
        }, {
          name:'李四',
          sex:'女',
          province: '130000',
          city: '130200',
          area: '130202',
        }
      ]
      this.$nextTick(()=>{
        //放在数据加载完后执行
        this.$refs.crud.dicInit('cascader');
      })
    }
}
</script>
```

[表格列配置项](https://v2.avuejs.com/crud/crud-column/) [操作栏配置](https://v2.avuejs.com/crud/crud-menu/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号