Contextmenu 右键菜单
================

Tips

2.9.8+

* 张三
* 李四
* 王五

* 菜单1
* 菜单2
* 菜单3
* 菜单4
* 菜单5

利用`v-contextmenu`指令传入相关参数即可

```html
<ul>
  <li v-for="(item,index) in list" :key="index" class="el-dropdown-menu__item"
    v-contextmenu="{id:'dialog',event:handleEvent,value:item,hide:handleHide}">
    {{item.name}}
  </li>
</ul>
<ul class="el-dropdown-menu el-popper" id="dialog" style="display:none">
  <li class="el-dropdown-menu__item" @click="handleClick1">
    <i class="el-icon-eleme"></i>菜单1
  </li>
  <li class="el-dropdown-menu__item" @click="handleClick2">
    <i class="el-icon-user"></i>菜单2
  </li>
  <li class="el-dropdown-menu__item" @click="handleClick3">
    <i class="el-icon-goods"></i>菜单3
  </li>
  <li class="el-dropdown-menu__item el-dropdown-menu__item--divided" @click="handleClick4">
    <i class="el-icon-circle-check"></i>菜单4
  </li>
  <li class="el-dropdown-menu__item" @click="handleClick4">
    菜单5
  </li>
</ul>
<script>
export default {
  data() {
    return {
      form: {},
      list: [
        { name: '张三' },
        { name: '李四' },
        { name: '王五' }
      ]
    }
  },
  created() {
    setTimeout(() => {
      this.list[0].name = 'small'
    }, 1000)
  },
  methods: {
    handleHide(row) {
      this.$message.success('隐藏回调信息' + JSON.stringify(row))
    },
    handleEvent(row, done) {
      this.form = row;
      done();
      this.$message.success('回调信息' + JSON.stringify(row))
    },
    handleClick1() {
      this.$message.success('菜单1' + JSON.stringify(this.form))
    },
    handleClick2() {
      this.$message.success('菜单2' + JSON.stringify(this.form))
    },
    handleClick3() {
      this.$message.success('菜单3' + JSON.stringify(this.form))
    },
    handleClick4() {
      this.$message.success('菜单4' + JSON.stringify(this.form))
    },
  }
}
</script>
```