统计合计
====

配置相应的属性后，在表格末尾即可达到统计合计功能

普通用法
------------------------------------------------------------------------------------

`showSummary`设置为`true`即可开启统计合计功能，`sumColumnList`属性配置需要计算的表格列配置，其中`name`为列的`prop`值，`type`为需要计算的类型，目前支持（合计 / 平均 / 统计）三个大功能，后期将会加强表格的计算能力

```vue
<avue-crud :option="option" :data="data"></avue-crud>
<script>
export default {
  data(){
    return {
       data:[
         {
          sum: 5,
          avg: 10,
          count: 2,
         },{
          sum: 15,
          avg: 20,
          count: 1,
         }
       ],
       option:{
          index:true,
          showSummary: true,
          sumColumnList: [
            {
              label:'自定义前缀:',
              name: 'sum',
              type: 'sum',
              decimals:1
            },
            {
              name: 'avg',
              type: 'avg'
            },
            {
              name: 'count',
              type: 'count'
            }
          ],
          column: [{
            label: '相加',
            prop: 'sum'
          },
          {
            label: '平均值',
            prop: 'avg'
          },
          {
            label: '统计',
            prop: 'count'
          }]
       }
    }
  }
}
</script>
```

自定义计算
----------------------------------------------------------------------------------------------

```vue
<avue-crud  :option="option" :data="data" :summary-method="summaryMethod" @selection-change="selectionChange"></avue-crud>
<script>
export default {
  data(){
    return {
       selectList:[],
       data:[
         {
          sum: 5,
          avg: 10,
          count: 2,
         },{
          sum: 15,
          avg: 20,
          count: 1,
         }
       ],
       option:{
          selection:true,
          index:true,
          showSummary: true,
          column: [{
            label: '相加',
            prop: 'sum'
          },
          {
            label: '平均值',
            prop: 'avg'
          },
          {
            label: '统计',
            prop: 'count'
          }]
       }
    }
  },
  methods:{
    selectionChange(list){
      this.selectList=list;
    },
    summaryMethod({ columns, data }){
      const sums = [];
      if (columns.length > 0) {
        columns.forEach((column, index) => {
          let prop=column.property
          if (['sum','avg','count'].includes(prop) ) {
            let values = this.selectList.map(item => Number(item[prop] || 0));
            let all=values.length!==0? sums[index] = values.reduce((a, b)=>{
              return a + b;
            }):0
            if(prop=='sum'){
              sums[index]=all
            }else if(prop=='avg'){
              sums[index]=all/values.length || 0
            }else if(prop=='count'){
              sums[index]=values.length
            }
          } else {
            sums[index] = '-'
          }
        });
      }
      return sums;
    }
  }
}
</script>
```

[卡片模式](https://v2.avuejs.com/crud/crud-grid/) [导入导出](https://v2.avuejs.com/crud/crud-export/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号