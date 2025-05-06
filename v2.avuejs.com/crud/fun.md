增删改查方法
======

Tips

可以参考[自定义按钮](https://v2.avuejs.com/crud/crud-btn-slot.html)更加灵活

新增数据
------------------------------------------------------------------------------------

新增数据保存回调`rowSave`方法,执行`done`关闭当前表单,`loading`用于添加失败后不关闭弹窗，重新提交

```vue
<avue-crud :data="data" :option="option" @row-save="rowSave"></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name:'张三',
            sex:'男'
          }, {
            id:2,
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          editBtn:false,
          delBtn:false,
          addBtnText:'新增数据',
          addBtnIcon:'el-icon-user',
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        },
      };
    },
    methods: {
     rowSave(form,done,loading){
        this.$message.success('模拟网络请求')
        setTimeout(()=>{
          this.$message.success('关闭按钮等待');
          loading();
        },1000)
        setTimeout(()=>{
          this.$message.success('新增数据'+ JSON.stringify(form));
          done(form);
        },2000)
      }
    }
}
</script>
```

修改数据
------------------------------------------------------------------------------------

修改数据保存回调`rowUpdate`方法,执行`done`关闭当前表单,`loading`用于添加失败后不关闭弹窗，重新提交

```vue
<avue-crud :data="data" :option="option" @row-update="rowUpdate"></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name:'张三',
            sex:'男'
          }, {
            id:2,
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          addBtn:false,
          delBtn:false,
          editBtnText:'修改数据',
          editBtnIcon:'el-icon-user',
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        },
      };
    },
    methods: {
      rowUpdate(form,index,done,loading){
        this.$message.success('模拟网络请求')
        setTimeout(()=>{
          this.$message.success('关闭按钮等待');
          loading();
        },1000)
        setTimeout(()=>{
          this.$message.success('编辑数据'+ JSON.stringify(form)+'数据序号'+index);
          done(form);
        },2000)
      }
    }
}
</script>
```

删除数据
------------------------------------------------------------------------------------

修改数据保存回调`rowDel`方法

```vue
<avue-crud :data="data" :option="option" @row-del="rowDel"></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name:'张三',
            sex:'男'
          }, {
            id:2,
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          editBtn:false,
          addBtn:false,
          delBtnText:'删除数据',
          delBtnIcon:'el-icon-user',
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        },
      };
    },
    methods: {
      rowDel(form,index){
         this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => { });
      }
    }
}
</script>
```

刷新数据
------------------------------------------------------------------------------------

Tips

这里刷新按钮回调可以配合[分页参数和方法](https://v2.avuejs.com/crud/crud-page.html)去请求数据

点击刷新按钮回调`refresh-change`方法

```vue
<avue-crud :data="data" :option="option" @refresh-change="refreshChange"></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name:'张三',
            sex:'男'
          }, {
            id:2,
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          addBtn:false,
          menu:false,
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        },
      };
    },
    methods: {
      refreshChange(){
        this.$message.success('刷新回调');
     }
    }
}
</script>
```

综合用法
------------------------------------------------------------------------------------

在操作过程中把数据放入`done`中,可以直接修改本地数据，做到及时刷新

```vue
<avue-crud :data="data" :option="option" 
                @refresh-change="refreshChange"
                 @row-save="rowSave"
                 @row-update="rowUpdate"
                 @row-del="rowDel"></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name:'张三',
            sex:'男'
          }, {
            id:2,
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        },
      };
    },
    methods: {
    refreshChange(){
        this.$message.success('刷新回调');
     },
     rowSave(form,done,loading){
        form.id=new Date().getTime();
        this.$message.success('模拟网络请求')
        setTimeout(()=>{
          this.$message.success('关闭按钮等待');
          loading();
        },1000)
        setTimeout(()=>{
          this.$message.success('新增数据'+ JSON.stringify(form));
          done(form);
        },2000)
      },
      rowDel(form,index,done){
         this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          done(form)
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => { });
      },
      rowUpdate(form,index,done,loading){
        this.$message.success('模拟网络请求')
        setTimeout(()=>{
          this.$message.success('关闭按钮等待');
          loading();
        },1000)
        setTimeout(()=>{
          this.$message.success('编辑数据'+ JSON.stringify(form)+'数据序号'+index);
          done(form);
        },2000)
      },
    }
}
</script>
```

[操作栏配置](https://v2.avuejs.com/crud/crud-menu/) [按钮文案和图标](https://v2.avuejs.com/crud/crud-text/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本。关注Avue Cloud公众号。