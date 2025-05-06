inputMap地图选择器
=============

<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<!-- 高德地图api更新必须配合安全密钥使用 -->
<script>
  window._AMapSecurityConfig = {
    securityJsCode: 'xxxxx',
  }
</script>
<script type="text/javascript" src='https://webapi.amap.com/maps?v=1.4.11&key=xxxxxxxx&plugin=AMap.PlaceSearch'></script>
<script src="https://webapi.amap.com/ui/1.0/main.js?v=1.0.11"></script>

值:[ 113.10235504165291, 41.03624227495205, "内蒙古自治区乌兰察布市集宁区新体路街道顺达源广告传媒" ]

<el-row :span="24">
  <el-col :span="6">
   值:{{form}}<br/>
   <avue-input-map  :params="params" placeholder="请选择地图" v-model="form" ></avue-input-map>
  </el-col>
</el-row>
<script>
export default {
    data() {
      return {
        //高德初始化参数
        params:{
          zoom: 10,
          // zoomEnable: false,
          // dragEnable: false,
        },
        form:[ 113.10235504165291, 41.03624227495205, "内蒙古自治区乌兰察布市集宁区新体路街道顺达源广告传媒" ] ,
      }
    }
}
</script>

[inputIcon图标选择器](https://v2.avuejs.com/component/input-icon/) [inputTabel表格选择器](https://v2.avuejs.com/component/input-table/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号