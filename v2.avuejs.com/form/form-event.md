表单组件事件
======

Tips

2.6.0+

* `change`事件
* `click`事件
* `focus`事件
* `blur`事件
* `enter`事件

组件事件
------

目前组件有 5 个事件`change`,`click`,`focus`,`blur`,`enter`

```vue
<avue-form :option="option" v-model="obj"></avue-form>
<script>
  export default {
    data() {
      return {
        obj: {},
        data: [],
        option: {
          column: [
            {
              label: "省份",
              prop: "name",
              type: "select",
              props: {
                label: "name",
                value: "code",
              },
              dicUrl: `https://cli.avuejs.com/api/area/getProvince`,
              change: ({ value, column, item, dic }) => {
                this.$message.success("change事件查看控制台");
                console.log("值改变", value, column, item, dic);
              },
              click: ({ value, column }) => {
                this.$message.success("click事件查看控制台");
                console.log("点击事件", value, column);
              },
              focus: ({ value, column }) => {
                this.$message.success("focus事件查看控制台");
                console.log("获取焦点", value, column);
              },
              blur: ({ value, column }) => {
                this.$message.success("blur事件查看控制台");
                console.log("失去焦点", value, column);
              },
              enter: ({ value, column }) => {
                this.$message.success("enter事件查看控制台");
                console.log("回车事件", value, column);
              },
            },
          ],
        },
      };
    },
  };
</script>
```

组件对象
------

Tips

2.6.2+

Tips

* [input-table 组件实际用法](https://v2.avuejs.com/form/form-input-table.html)

```vue
<avue-form ref="form" v-model="form" :option="option"></avue-form>

<script>
  export default {
    data() {
      return {
        form: {},
        option: {
          labelWidth: 120,
          column: [
            {
              label: "测试框",
              prop: "text",
            },
          ],
        },
      };
    },
    mounted() {
      this.$message.success("查看控制台");
      console.log("text的ref对象");
      console.log(this.$refs.form.getPropRef("text").$refs.temp);
    },
  };
</script>
```

组件交互
------

Tips

2.8.10+  
2.13.0+ control 支持`promise`类型

可以写判断逻辑，返回对应改变的对象属性，

```vue
<avue-form :option="option" v-model="form"></avue-form>
<script>
  export default {
    data() {
      return {
        form: {
          text1: 0,
        },
        option: {
          column: [
            {
              label: "内容1",
              prop: "text1",
              type: "radio",
              control: (val, form) => {
                if (val === 0) {
                  return {
                    text2: {
                      display: true,
                    },
                    text3: {
                      label: "内容3",
                    },
                  };
                } else {
                  return {
                    text2: {
                      display: false,
                    },
                    text3: {
                      label: "有没有发现我变了",
                    },
                  };
                }
              },
              dicData: [
                {
                  label: "显示",
                  value: 0,
                },
                {
                  label: "隐藏",
                  value: 1,
                },
              ],
            },
            {
              label: "内容2",
              prop: "text2",
              display: true,
              control: (val, form) => {
                return new Promise((resolve) => {
                  if (val) {
                    resolve({
                      text1: {
                        label: "改变内容1",
                      },
                    });
                  } else {
                    resolve({
                      text1: {
                        label: "内容1",
                      },
                    });
                  }
                });
              },
            },
            {
              label: "内容3",
              prop: "text3",
            },
          ],
        },
      };
    },
  };
</script>
```

[表单数据格式](https://v2.avuejs.com/form/form-data/) [表单高级用法](https://v2.avuejs.com/form/form-ajax/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号