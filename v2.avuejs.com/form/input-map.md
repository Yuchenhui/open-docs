Map坐标选择器
========

<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<!-- 高德地图api更新必须配合安全密钥使用 -->
<script>
  window._AMapSecurityConfig = {
    securityJsCode: 'xxxxx',
  }
</script>
<script type="text/javascript" src='https://webapi.amap.com/maps?v=1.4.11&key=xxxxxxxx&plugin=AMap.PlaceSearch'></script>
<script src="https://webapi.amap.com/ui/1.0/main.js?v=1.0.11"></script>

基础用法
------------------------------------------------------------------------------------------

```vue
<avue-form :option="option" ></avue-form>

<script>
export default{
  data() {
    return {
      option: {
          column: [
            {
              label: '坐标',
              prop: 'map',
              type: 'map',
            }
          ]
      }
    }
  }
}
</script>
```

默认值
--------------------------------------------------------------------------------

`value`属性可以提供一个初始化的默认值

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label: '坐标',
            prop: 'map',
            type: 'map',
            value:[ 113.10235504165291, 41.03624227495205, "内蒙古自治区乌兰察布市集宁区新体路街道顺达源广告传媒" ]
         }
        ]
      }
    }
  }
}
</script>
```

禁用状态
------------------------------------------------------------------------------------------

通过`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label: '坐标',
            prop: 'map',
            type: 'map',
            disabled:true
         }
        ]
      }
    }
  }
}
</script>
```

高德参数
------------------------------------------------------------------------------------------

```vue
<avue-form :option="option" v-model="form" ></avue-form>

<script>
export default{
  data() {
    return {
      form: {
        map: [ 113.10235504165291, 41.03624227495205, "内蒙古自治区乌兰察布市集宁区新体路街道顺达源广告传媒" ] 
      },
      option: {
          column: [
            {
              label: '坐标',
              prop: 'map',
              type: 'map',
              mapChange:(params)=>{
                console.log('高德参数',params)
              },
              //高德初始化参数
              params:{
                zoom: 10,
                zoomEnable: false,
                dragEnable: false,
              }
            }
          ]
      }
    }
  }
}
</script>
```

[Table表格选择器](https://v2.avuejs.com/form/form-input-table/) [Color颜色选择器](https://v2.avuejs.com/form/form-input-color/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)**
查看 Vue 3.x 的升级版本

关注Avue Cloud公众号