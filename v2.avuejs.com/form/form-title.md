Title标题
=======

... 2021-7-29 Less than 1 minute

* * *

[#](https://v2.avuejs.com/form/form-title/#title%E6%A0%87%E9%A2%98)  
Title标题
============================================================================

Tips

2.6.15+

[#](https://v2.avuejs.com/form/form-title/#%E6%99%AE%E9%80%9A%E7%94%A8%E6%B3%95)  
普通用法
--------------------------------------------------------------------------------------

```vue
<avue-form v-model="form" :option="option" ></avue-form>

<script>
export default {
    data() {
      return {
        form:{
          title:'我是头部标题',
          title1:'我是尾部标题'
        },
        option:{
          column: [
            {
              label: "",
              labelWidth:20,
              type:'title',
              prop: "title",
              span:24,
              styles:{
                color:'red',
                fontSize:'24px'
              }
            },
            {
              label:'输入框',
              prop:'text'
            },
            {
              label: "",
              labelWidth:20,
              type:'title',
              prop: "title1",
              span:24,
              styles:{
                color:'green',
                fontSize:'18px'
              }
            }
          ]
        }
      };
    }
}
</script>
```

[Upload 附件上传](https://v2.avuejs.com/form/form-upload/) [Array数组框](https://v2.avuejs.com/form/form-array/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号