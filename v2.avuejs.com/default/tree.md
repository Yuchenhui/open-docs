Tree 树型
=======

普通用法
-----------------------------------------------------------------------------------

{}

`option`配置属性,`data`为数据，`node-click`为点击事件

```vue
{{form}}
<avue-tree  ref="tree" :option="option" :data="data"  v-model="form" @node-click="nodeClick"  @node-contextmenu="nodeContextmenu">
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          data:[
            {
              value:0,
              label:'一级部门',
              children:[
                {
                  value:1,
                  label:'一级部门1',
                },{
                  value:2,
                  label:'一级部门2',
                }
              ]
            },{
              value:3,
              label:'二级部门',
              children:[
                {
                  value:4,
                  label:'二级部门1',
                },{
                  value:5,
                  label:'二级部门2',
                }
              ]
            }
          ],
          option:{
            defaultExpandAll:true,
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              },{
                label:'测试',
                prop:'test'
              }],
            }
          }
      }
  },
  mounted(){
    this.$refs.tree.setCurrentKey(0)
  },
  methods:{
    nodeContextmenu (data, node, comp) {
      this.$message.success(JSON.stringify(data))
    },
    nodeClick(data){
      this.$message.success(JSON.stringify(data))
    }
  }
}
</script>
```

多选
---------------------------------------------------------------

`multiple`配置为`true`即可开启多选，`check-change`方法为回调函数

```vue
<avue-tree  ref="tree" :option="option" :data="data"  v-model="form" @check-change="checkChange">
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          data:[
            {
              value:0,
              label:'一级部门',
              children:[
                {
                  value:1,
                  label:'一级部门1',
                },{
                  value:2,
                  label:'一级部门2',
                }
              ]
            },{
              value:3,
              label:'二级部门',
              children:[
                {
                  value:4,
                  label:'二级部门1',
                },{
                  value:5,
                  label:'二级部门2',
                }
              ]
            }
          ],
          option:{
            defaultExpandAll:true,
            multiple:true,
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              },{
                label:'测试',
                prop:'test'
              }],
            }
          }
      }
  },
  mounted(){
    this.$refs.tree.setCheckedKeys([0])
  },
  methods:{
    checkChange(data, checked, indeterminate){
      this.$message.success(JSON.stringify(data))
    }
  }
}
</script>
```

配置属性
-----------------------------------------------------------------------------------

```vue
<avue-tree  :option="option" :data="data"  v-model="form">
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          data:[
            {
              value:0,
              label:'一级部门',
              children:[
                {
                  value:1,
                  label:'一级部门1',
                },{
                  value:2,
                  label:'一级部门2',
                }
              ]
            },{
              value:3,
              label:'二级部门',
              children:[
                {
                  value:4,
                  label:'二级部门1',
                },{
                  value:5,
                  label:'二级部门2',
                }
              ]
            }
          ],
          option:{
            title:'我是标题',
            filterText:"搜索关键字自定义",
            defaultExpandAll:true,
            addBtnText:'新增自定义文案',
            editBtnText:'修改自定义文案',
            delBtnText:'删除自定义文案',
            defaultExpandedKeys:[1],
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              }],
            },
            props:{
              labelText:'标题',
              label:'label',
              value:'value',
              children:'children'
            }
          }
      }
  }
}
</script>
```

打开前和关闭前
-----------------------------------------------------------------------------------------------------------------

{}

`before-open`打开前的方法,`before-close`关闭前的方法

```vue
{{form}}
<avue-tree :before-open="beforeOpen" :before-close="beforeClose"  :option="option" :data="data"  v-model="form" >
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          data:[
            {
              value:0,
              label:'一级部门',
              children:[
                {
                  value:1,
                  label:'一级部门1',
                },{
                  value:2,
                  label:'一级部门2',
                }
              ]
            },{
              value:3,
              label:'二级部门',
              children:[
                {
                  value:4,
                  label:'二级部门1',
                },{
                  value:5,
                  label:'二级部门2',
                }
              ]
            }
          ],
          option:{
            defaultExpandAll:true,
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              },{
                label:'测试',
                prop:'test'
              }],
            }
          }
      }
  },
  methods:{
    beforeOpen(done, type) {
       this.$alert(`我是${type}`, {
          confirmButtonText: '确定',
        callback: action => {
          if(['view','edit'].includes(type)){
            // 查看和编辑逻辑
          }else{
            //新增逻辑
            this.form.test='初始化赋值'
          }
          done();
        }
      });
    },
    beforeClose(done, type) {
       this.$confirm('确认关闭？')
        .then(_ => {
          done();
        })
        .catch(_ => {});
    },
  }
}
</script>
```

事件和自定义
-------------------------------------------------------------------------------------------------------

`option`配置属性即可,`data`为可配置项目，具体参考下表文档

```vue
<avue-tree  :option="option" :data="data" :filter-node-method="filterNodeMethod" @update="update" @save="save" @del="del" v-model="form">
  <span class="el-tree-node__label" slot-scope="{ node, data }">
    <span>
      <i class="el-icon-user-solid"></i>
      {{ (node || {}).label }}
    </span>
  </span>
  <template slot-scope="{node}" slot="menu">
    <div class="avue-tree__item" @click="tip(node)">自定义按钮</div>
  </template>
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          data:[
            {
              value:0,
              label:'一级部门',
              children:[
                {
                  value:1,
                  label:'一级部门1',
                },{
                  value:2,
                  label:'一级部门2',
                }
              ]
            },{
              value:3,
              label:'二级部门',
              children:[
                {
                  value:4,
                  label:'二级部门1',
                },{
                  value:5,
                  label:'二级部门2',
                }
              ]
            }
          ],
          option:{
            defaultExpandAll:true,
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              }],
            },
          }
      }
  },
  methods:{
    filterNodeMethod(value,data){
        if (!value) return true;
        return data.label.indexOf(value) !== -1;
    },
    tip(node){
        this.$message.success(JSON.stringify(node.data))
    },
    del(data,done){
      this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$message.success('删除回调')
        done();
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消删除'
        });          
      });
    },
    update(node,data,done,loading){
      this.$message.success('更新回调')
      done();
    },
    save(node,data,done,loading){
      this.$message.success('新增回调')
      this.form.id = new Date().getTime();
      this.form.value=new Date().getTime();
      this.form.children=[];
      done();
    }
  }
}
</script>
```

拖拽
---------------------------------------------------------------

```vue
<avue-tree @node-drag-start="handleDragStart"
  @node-drag-enter="handleDragEnter"
  @node-drag-leave="handleDragLeave"
  @node-drag-over="handleDragOver"
  @node-drag-end="handleDragEnd"
  @node-drop="handleDrop" :option="option" :data="data">
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          data:[
            {
              value:0,
              label:'一级部门',
              children:[
                {
                  value:1,
                  label:'一级部门1',
                },{
                  value:2,
                  label:'一级部门2',
                }
              ]
            },{
              value:3,
              label:'二级部门',
              children:[
                {
                  value:4,
                  label:'二级部门1',
                },{
                  value:5,
                  label:'二级部门2',
                }
              ]
            }
          ],
          option:{
            draggable:true,
            defaultExpandAll:true,
            allowDrop:(draggingNode, dropNode, type)=> {
              if (dropNode.data.label === '一级部门2') {
                return type !== 'inner';
              } else {
                return true;
              }
            },
            allowDrag:(draggingNode)=> {
              return draggingNode.data.label.indexOf('一级部门2') === -1;
            },
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              }],
            },
          }
      }
  },
  methods:{
   handleDragStart(node, ev) {
        console.log('drag start', node);
      },
      handleDragEnter(draggingNode, dropNode, ev) {
        console.log('tree drag enter: ', dropNode.label);
      },
      handleDragLeave(draggingNode, dropNode, ev) {
        console.log('tree drag leave: ', dropNode.label);
      },
      handleDragOver(draggingNode, dropNode, ev) {
        console.log('tree drag over: ', dropNode.label);
      },
      handleDragEnd(draggingNode, dropNode, dropType, ev) {
        console.log('tree drag end: ', dropNode && dropNode.label, dropType);
      },
      handleDrop(draggingNode, dropNode, dropType, ev) {
        console.log('tree drop: ', dropNode.label, dropType);
      }
  }
}
</script>
```

权限
---------------------------------------------------------------

```vue
<avue-tree  :permission="getPermission" :option="option" :data="data">
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          data:[
            {
              value:0,
              label:'一级部门',
              children:[
                {
                  value:1,
                  label:'一级部门1',
                },{
                  value:2,
                  label:'一级部门2',
                }
              ]
            },{
              value:3,
              label:'二级部门',
              children:[
                {
                  value:4,
                  label:'二级部门1',
                },{
                  value:5,
                  label:'二级部门2',
                }
              ]
            }
          ],
          option:{
            defaultExpandAll:true,
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              }],
            },
          }
      }
  },
  methods:{
    getPermission(key, data) {
      if (key == "addBtn"&&data.value==0) { return false; }
      return true;
    }
  }
}
</script>
```

懒加载
-------------------------------------------------------------------------

`lazy`设置为`true`即可，后在`treeLoad`函数里面处理逻辑，具体看下面例子

```vue
<avue-tree :option="option" v-model="form">
</avue-tree>
<script>
export default {
    data () {
      return {
          form:{},
          option:{
            formOption:{
              labelWidth:100,
              column:[{
                  label:'自定义项',
                  prop:'label'
              }],
            },
            lazy: true,
            treeLoad: function (node, resolve) {
              if (node.level === 0) {
                return resolve([{ is_show: true, label: 'region', value: new Date().getTime() }]);
              }
              if (node.level > 2) return resolve([]);
              setTimeout(() => {
                const data = [{
                  label: 'leaf',
                  is_show: true,
                  value: new Date().getTime(),
                  leaf: true
                }, {
                  is_show: true,
                  value: new Date().getTime(),
                  label: 'zone'
                }];

                resolve(data);
              }, 500);
            }
          }
      }
  }
}
</script>
```

Variables
-------------------------------------------------------------

| 参数  | 说明  | 类型  | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| option | 组件配置属性，详情见下面Option属性 | Object | —   | —   |
| data | 存放结构体的数据 | Array | —   | —   |

Option Attributes
-----------------------------------------------------------------------------

| 参数  | 说明  | 类型  | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| defaultExpandAll | 是否展开节点 | Boolean | false / true | false |
| dialogWidth | 弹出框宽度 | String | \-  | 50% |
| formOption | 自定义form表单，具体参考avue-form组件(默认自带一个标题的column，可以根据配置去修改) | Object | \-  | \-  |
| menu | 菜单栏 | Boolean | false / true | true |
| addBtn | 新增按钮 | Boolean | false / true | true |
| editBtn | 编辑按钮 | Boolean | false / true | true |
| delBtn | 修改按钮 | Boolean | false / true | true |
| props | 配置选项，具体看下表 | object | \-  | \-  |
| filter | 是否显示搜索框 | Boolean | false / true | true |

Column Attributes
-----------------------------------------------------------------------------

| 参数  | 说明  | 类型  | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| label | 节点的名称 | String | \-  | \-  |
| value | 节点的值 | String | \-  | \-  |
| id  | 节点主键 | String | \-  | \-  |
| children | 子节点 | Array | \-  | \-  |

Props Attributes
---------------------------------------------------------------------------

| 参数  | 说明  | 类型  | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| label | 指定节点标签为节点对象的某个属性值 | string | —   | —   |
| labelText | 弹窗添加节点的名称 | string | \-  | 名称  |
| children | 指定子树为节点对象的某个属性值 | string | —   | —   |
| value | 指定节点选择框的值也作为节点的nodeKey | string | —   | —   |

Events
-------------------------------------------------------

| 事件名 | 说明  | 参数  |
| --- | --- | --- |
| save | 新增节点回调 | parent, data, done,loading |
| update | 修改节点回调 | parent, data, done,loading |
| del | 删除节点回调 | data, done |
| before-open | 打开前回调 | done, type |
| before-close | 关闭前回调 | done, type |
| node-click | 节点被点击时的回调 | 共三个参数，依次为：传递给 `data` 属性的数组中该节点所对应的对象、节点对应的 Node、节点组件本身。 |
| check-change | 节点选中状态发生变化时的回调 | 共三个参数，依次为：传递给 `data` 属性的数组中该节点所对应的对象、节点本身是否被选中、节点的子树中是否有被选中的节点 |

Methods
---------------------------------------------------------

`Tree` 内部使用了 Node 类型的对象来包装用户传入的数据，用来保存目前节点的状态。 `Tree` 拥有如下方法：

| 方法名 | 说明  | 参数  |
| --- | --- | --- |
| filter | 对树节点进行筛选操作 | 接收一个任意类型的参数，该参数会在 filter-node-method 中作为第一个参数 |
| updateKeyChildren | 通过 keys 设置节点子元素，使用此方法必须设置 node-key 属性 | (key, data) 接收两个参数，1. 节点 key 2. 节点数据的数组 |
| getCheckedNodes | 若节点可被选择（即 `show-checkbox` 为 `true`），则返回目前被选中的节点所组成的数组 | (leafOnly, includeHalfChecked) 接收两个 boolean 类型的参数，1. 是否只是叶子节点，默认值为 `false` 2. 是否包含半选节点，默认值为 `false` |
| setCheckedNodes | 设置目前勾选的节点，使用此方法必须设置 node-key 属性 | (nodes) 接收勾选节点数据的数组 |
| getCheckedKeys | 若节点可被选择（即 `show-checkbox` 为 `true`），则返回目前被选中的节点的 key 所组成的数组 | (leafOnly) 接收一个 boolean 类型的参数，若为 `true` 则仅返回被选中的叶子节点的 keys，默认值为 `false` |
| setCheckedKeys | 通过 keys 设置目前勾选的节点，使用此方法必须设置 node-key 属性 | (keys, leafOnly) 接收两个参数，1. 勾选节点的 key 的数组 2. boolean 类型的参数，若为 `true` 则仅设置叶子节点的选中状态，默认值为 `false` |
| setChecked | 通过 key / data 设置某个节点的勾选状态，使用此方法必须设置 node-key 属性 | (key/data, checked, deep) 接收三个参数，1. 勾选节点的 key 或者 data 2. boolean 类型，节点是否选中 3. boolean 类型，是否设置子节点 ，默认为 false |
| getHalfCheckedNodes | 若节点可被选择（即 `show-checkbox` 为 `true`），则返回目前半选中的节点所组成的数组 | \-  |
| getHalfCheckedKeys | 若节点可被选择（即 `show-checkbox` 为 `true`），则返回目前半选中的节点的 key 所组成的数组 | \-  |
| getCurrentKey | 获取当前被选中节点的 key，使用此方法必须设置 node-key 属性，若没有节点被选中则返回 null | —   |
| getCurrentNode | 获取当前被选中节点的 data，若没有节点被选中则返回 null | —   |
| setCurrentKey | 通过 key 设置某个节点的当前选中状态，使用此方法必须设置 node-key 属性 | (key) 待被选节点的 key，若为 null 则取消当前高亮的节点 |
| setCurrentNode | 通过 node 设置某个节点的当前选中状态，使用此方法必须设置 node-key 属性 | (node) 待被选节点的 node |
| getNode | 根据 data 或者 key 拿到 Tree 组件中的 node | (data) 要获得 node 的 key 或者 data |
| remove | 删除 Tree 中的一个节点，使用此方法必须设置 node-key 属性 | (data) 要删除的节点的 data 或者 node |
| append | 为 Tree 中的一个节点追加一个子节点 | (data, parentNode) 接收两个参数，1. 要追加的子节点的 data 2. 子节点的 parent 的 data、key 或者 node |
| insertBefore | 为 Tree 的一个节点的前面增加一个节点 | (data, refNode) 接收两个参数，1. 要增加的节点的 data 2. 要增加的节点的后一个节点的 data、key 或者 node |
| insertAfter | 为 Tree 的一个节点的后面增加一个节点 | (data, refNode) 接收两个参数，1. 要增加的节点的 data 2. 要增加的节点的前一个节点的 data、key 或者 node |

Scoped Slot
-----------------------------------------------------------------

| name | 说明  |
| --- | --- |
| menuBtn | 按钮的卡槽 |
| addBtn | 新增按钮卡槽 |
| \-  | 节点卡槽 |

[Calendar日历](https://v2.avuejs.com/default/calendar/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号