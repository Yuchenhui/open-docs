CRUD极简增删改查封装
============

CRUD极简增删改查封装

封装插件

```js
@/mixins/crud.js
export default (app, option = {}) => {
  let mixins = {
    data () {
      return {
        data: [],
        form: {},
        params: {},
        api: require(`@/api/${option.name}`),
        option: require(`@/option/${option.name}`).default(this),
        loading: false,
        page: {},
      }
    },
    computed: {
      bindVal () {
        return {
          ref: 'crud',
          option: this.option,
          data: this.data,
          tableLoading: this.loading
        }
      },
      onEvent () {
        return {
          'on-load': this.getList,
          'row-save': this.rowSave,
          'row-update': this.rowUpdate,
          'row-del': this.rowDel,
          'refresh-change': this.refreshChange,
          'search-reset': this.searchChange,
          'search-change': this.searchChange
        }
      },
      rowKey () {
        return option.rowKey || 'id'
      }
    },
    methods: {
      getList () {
        const callback = () => {
          this.loading = true;
          let pageParams = {}
          pageParams[option.pageNumber || 'pageNumber'] = this.page.currentPage
          pageParams[option.pageSize || 'pageSize'] = this.page.pageSize

          const data = Object.assign(pageParams, this.params)
          this.data = [];
          this.api[option.list || 'list'](data).then(res => {
            this.loading = false;
            let data;
            if (option.res) {
              data = option.res(res.data);
            } else {
              data = res.data.data
            }
            this.page.total = data[option.total || 'total'];
            const result = data[option.data || 'data'];
            this.data = result;
            if (this.listAfter) {
              this.listAfter(data)
            } else {
              this.$message.success('获取成功')
            }
          })
        }
        if (this.listBefore) {
          this.listBefore()
        }
        callback()
      },
      rowSave (row, done, loading) {
        const callback = () => {
          delete this.form.params;
          this.api[option.add || 'add'](this.form).then((data) => {
            this.getList();
            if (this.addAfter) {
              this.addAfter(data)
            } else {
              this.$message.success('新增成功')
            }
            done();
          }).catch(() => {
            loading()
          })
        }
        if (this.addBefore) {
          this.addBefore()
        }
        callback()
      },
      rowUpdate (row, index, done, loading) {
        const callback = () => {
          delete this.form.params;
          this.api[option.update || 'update'](row[this.rowKey], this.form, index).then((data) => {
            this.getList();
            if (this.updateAfter) {
              this.updateAfter(data)
            } else {
              this.$message.success('更新成功')
            }
            done()
          }).catch(() => {
            loading()
          })
        }
        if (this.updateBefore) {
          this.updateBefore()
        }
        callback()
      },
      rowDel (row, index) {
        const callback = () => {
          this.api[option.del || 'del'](row[this.rowKey], row).then((data) => {
            this.getList();
            if (this.delAfter) {
              this.delAfter(data, row, index)
            } else {
              this.$message.success('删除成功')
            }
          })
        }
        if (this.delBefore) {
          this.delBefore()
          callback()
        } else {
          this.$confirm(`此操作将永久删除序号【${index}】的数据, 是否继续?`, '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning'
          }).then(() => {
            callback()
          })
        }
      },
      searchChange (params, done) {
        if (done) done();
        this.params = params;
        this.page.currentPage = 1;
        this.getList();
      },
      refreshChange () {
        this.getList();
      }
    }
  }
  app.mixins = app.mixins || [];
  app.mixins.push(mixins)
  return app;
}
```

设置为全局方法

> 这样子每个模块里面不用全局引入，直接使用即可，这里作用到全局window下面

```js
main.js
import crudCommon from '@/mixins/crud'
window.$crudCommon = crudCommon;
```

使用方法

```js
@/option/system/params.js
export default (safe)=>{
  //safe => vue的this对象
  return {
    ...
    column:[]
    ....
  }
}

@/api/system/params.js
export const list = ()=>{}
export const add = ()=>{}
export const del = ()=>{}
export const update = ()=>{}

@/page/system/params.vue
<template>
  <basic-container>
    <avue-crud v-bind="bindVal"
               v-on="onEvent"
               v-model="form"
               :page.sync="page">
    </avue-crud>
  </basic-container>
</template>

<script>
export default window.$crudCommon({
  data () {
    return {}
  },
  methods: {
    //列表前操作方法
    listBefore(){},

    //列表后操作方法
    listAfter(){},

    //新增前操作方法
    addBefore () {
      this.form.createUser = 'small'
    },
    //新增后操作方法
    addAfter() {},

    //修改前操作方法
    updateBefore () {
      this.form.updateUser = 'small'
    },

    //修改后操作方法
    updateAfter() {},

    //删除前操作方法
    delBefore () {},

    //删除后操作方法
    delAfter() {},
  }
}, {
  name:'system/params',//模块名字
  list: 'list',//列表接口名字
  update: 'update',//更新接口名字
  add: 'add',//新增接口名字
  del: 'del',//删除接口名字
  rowKey: 'id',//主键
  pageNumber: 'pageNumber',//页码
  pageSize: 'pageSize',//页数
  res:(data)=>{
    return {
      total:0,
      data:[]
    }
  },//列表的结构
  total: 'total',//总页数
  data: 'list'//列表属性
})
</script>

<style lang="scss" scoped>
</style>
```