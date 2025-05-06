深层结构数据
======

2021-7-29 Less than 1 minute

* * *

深层结构数据
=========================================================================================================

Tips

2.6.11+

普通用法
-------------------------------------------------------------------------------------

`bing`绑定深层次的结构对象，`prop`也是需要填写

    <avue-crud :option="option" :data="data" ></avue-crud>
    
    <script>
    export default{
      data() {
        return {
          form:{},
          data: [{
            deep:{
              deep:{
                deep:{
                  value:'我是深结构'
                }
              }
            }
          }],
          option: {
            labelWidth: 120,
            column: [
              {
                label: '深结构',
                prop: 'test',
                bind:'deep.deep.deep.value'
              }
            ]
          }
        }
      }
    }
    </script>

[弹窗表单配置](https://v2.avuejs.com/crud/crud-form/) [卡片模式](https://v2.avuejs.com/crud/crud-grid/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号