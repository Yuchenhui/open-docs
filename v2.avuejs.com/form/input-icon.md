Icon图标选择器
=========

基础用法
-------------------------------------------------------------------------------------------

图标集合参考例子配置`iconList`属性

```vue
<avue-form :option="option"> </avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
          {
            label: '图标选择器',
            prop: 'icon',
            type: 'icon',
            iconList: [
              {
                label: '基本图标',
                list: [
                  { label: '名称1', value: 'el-icon-info' },
                  { label: '名称2', value: 'el-icon-error' },
                  { label: '名称3', value: 'el-icon-success' },
                  { label: '名称4', value: 'el-icon-warning' },
                  { label: '名称5', value: 'el-icon-question' }
                ]
              },
              {
                label: '方向图标',
                list: ['el-icon-info', 'el-icon-back', 'el-icon-arrow-left', 'el-icon-arrow-down', 'el-icon-arrow-right', 'el-icon-arrow-up']
              },
              {
                label: '符号图标',
                list: ['el-icon-plus', 'el-icon-minus', 'el-icon-close', 'el-icon-check']
              }
            ]
          }
        ]
      }
    }
  }
}
</script>
```

默认值
---------------------------------------------------------------------------------

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
            label: '图标',
            prop: 'icon',
            type: 'icon',
            value: 'el-icon-user',
            iconList: [
              {
                label: '符号图标',
                list: ['el-icon-plus', 'el-icon-minus', 'el-icon-close', 'el-icon-check']
              }
            ]
          }
        ]
      }
    }
  }
}
</script>
```

禁用状态
-------------------------------------------------------------------------------------------

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
            label: '图标',
            prop: 'icon',
            type: 'icon',
            disabled: true
          }
        ]
      }
    }
  }
}
</script>
```

其他图标库
-----------------------------------------------------------------------------------------------------

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<!-- 引入阿里巴巴的图表库iconfont和svg图标后，直接使用图标名即可，记得加前缀 -->
<link rel="stylesheet" href="https://at.alicdn.com/t/font_567566_pwc3oottzol.css">
<script src="//at.alicdn.com/t/font_2621503_zcbiqy2g1i.js"></script>
```

```vue
<avue-form :option="option"> </avue-form>

<script>
export default {
  data() {
    return {
      option: {
        column: [
          {
            label: '图标选择器',
            prop: 'icon',
            type: 'icon',
            iconList: [
              {
                label: '阿里图标-Symbol图标',
                list: [
                  { label: '机构', value: '#icon-jigou' },
                  { label: '短信管理', value: '#icon-duanxinguanli' },
                  { label: '发票管理系统', value: '#icon-fapiaoguanlixitong' },
                  { label: '角色', value: '#icon-jiaose' },
                  { label: '黑名单', value: '#icon-heimingdan2' },
                  { label: 'KHCFDC_附件', value: '#icon-fujian4' },
                  { label: '文档', value: '#icon-wendang3' },
                  { label: '刷卡', value: '#icon-shuaka' },
                  { label: '停车', value: '#icon-tingche3' },
                  { label: '对象存储OSS', value: '#icon-duixiangcunchuOSS' },
                  { label: '反馈', value: '#icon-fankui2' },
                  { label: '短信', value: '#icon-ziyuan1' },
                  { label: '对象存储服务', value: '#icon-beikongshuiwupingtaimenhu-tubiao_duixiangcunchufuwu' },
                  { label: '数据库_jurassic', value: '#icon-jurassic_data' },
                  { label: '日志', value: '#icon-rizhi1' },
                  { label: '权限', value: '#icon-quanxian4' },
                  { label: '订单', value: '#icon-5' },
                  { label: '机构', value: '#icon-jigou1' },
                  { label: '机构人员', value: '#icon-jigourenyuan' },
                  { label: '角色管理', value: '#icon-jiaoseguanli4' },
                  { label: '角色管理', value: '#icon-jiaoseguanli5' },
                  { label: '数据监控', value: '#icon-shujujiankong' },
                  { label: '活动展示', value: '#icon-huodongzhanshi' },
                  { label: 'vip invitation', value: '#icon-vipinvitation' }
                ]
              },
              {
                label: '阿里云图标',
                list: [
                  'iconfont icon-zhongyingwen',
                  'iconfont icon-rizhi1',
                  'iconfont icon-bug',
                  'iconfont icon-qq1',
                  'iconfont icon-weixin1'
                ]
              }
            ]
          }
        ]
      }
    }
  }
}
</script>
```