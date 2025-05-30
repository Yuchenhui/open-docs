DataPay 数据展示
============

Tips

1.0.2+

```vue
<avue-data-pay :option="option"></avue-data-pay>
<script>
export default {
  data(){
    return {
      option: {
        span: 8,
        data: [
          {
            title: '后台模版',
            src: 'images/vip1.png',
            money: '999999',
            dismoney: '999999',
            tip: '/永久',
            color: '#808695',
            subtext: '购买',
            click: function (item) {
              alert(JSON.stringify(item));
            },
            list: [
              {
                title: '面向全屏幕尺寸的响应式适配能力',
                check: true,
                tip: `<h2>后台管理模版 - <small>点击红色字体即可预览</small></h2><br/>
                1.用户名登录/验证码登录/第三方登陆(QQ, 微信)/人脸识别/多种登录方式。<br/><br/>
                2.全新的前端错误日志监控机制<br/><br/>
                3.灵活的10 + 多款主题自由配置<br/><br/>
                4.路由权限、菜单权限、登录权限<br/><br/>
                5.前端路由动态服务端加载和无限极动态路由加载。<br/><br/>
                6.模块的可拆卸化, 达到开箱即用<br/><br/>`,
              },
              {
                title: '支持IE9+等系列浏览器',
                check: true,
              },
              {
                title: '全新的前端错误日志监控机制',
                check: true,
              },
              {
                title: '基于最新的avue底层开发',
                check: true,
              },
              {
                title: '前端路由动态服务端加载',
                check: true,
              },
              {
                title: '灵活的多款主题自由配置',
                check: true,
              },
              {
                title: '模块的可拆卸化,达到开箱即用',
                check: true,
              },
              {
                title: '免费的私人git私服',
                check: true,
              },
              {
                title: '专属会员群',
                check: true,
              },
              {
                title: '前端最新干货分享',
                check: true,
              },
              {
                title: '赠送 Avue.js 脚手架文档（价值¥59.99）',
                href: 'https://www.kancloud.cn/smallwei/avue',
                check: true,
              },
              {
                title: '赠送 Avue 修仙系列视频教程',
                href: 'https://www.bilibili.com/video/av24644922',
                check: true,
              }
            ]
          },
          {
            title: 'Avuex源码',
            src: 'images/vip2.png',
            color: '#ffa820',
            money: '999999999',
            dismoney: '999999',
            tip: '/永久',
            subtext: '购买',
            click: function (item) {
              alert(JSON.stringify(item));
            },
            list: [
              {
                title: '一键集成表格的导出excel,打印,等功能',
                check: true,
              },
              {
                title: '底层代码可重用轻松对接多个UI框架',
                check: true,
              },
              {
                title: '底层更加完善的开发错误调试机制',
                check: true,
              },
              {
                title: '一套代码多个终端自适应',
                check: true,
              },
              {
                title: '一键集成表格的导出excel，打印，等常用功能',
                check: true,
              },
              {
                title: '表格的批量操作,表单的级联操作更加便捷',
                check: true,
              },
              {
                title: '新增大量常用组件（搜索，选项卡）',
                check: true,
              },
              {
                title: '新增大量全新可配置的骚属性',
                check: true,
              },
              {
                title: '丰富的数据展示模版组件包',
                check: true,
              },
              {
                title: '专属的开发者文档，助你快速掌握',
                check: true,
              },
              {
                title: '赠送 Avue.js 脚手架文档（价值¥59.99）',
                href: 'https://www.kancloud.cn/smallwei/avue',
                check: true,
              },
              {
                title: '赠送 Avue 修仙系列视频教程',
                href: 'https://www.bilibili.com/video/av24644922',
                check: true,
              }
            ]
          },
          {
            title: '全家桶',
            src: 'images/vip3.png',
            color: '#ef4868',
            money: '999999',
            dismoney: '999999',
            tip: '/永久',
            subtext: '购买',
            click: function (item) {
              alert(JSON.stringify(item));
            },
            list: [
              {
                title: '授权商业化开发,永久更新授权使用',
                check: true,
              },
              {
                title: '后期更新和新产品将全部免费',
                check: true,
              },
              {
                title: '拥有avue系列的全部特权和全部源码（包括avuex）',
                check: true,
              },
              {
                title: '提供远程技术支持和问题解答',
                check: true,
              },
              {
                title: '赠送 Avue.js 脚手架文档（价值¥59.99）',
                href: 'https://www.kancloud.cn/smallwei/avue',
                check: true,
              },
              {
                title: '赠送 Avue 修仙系列视频教程',
                href: 'https://www.bilibili.com/video/av24644922',
                check: true,
              }
            ]
          }
        ]
      },
    }
  }
}
</script>
```

Attributes
----------

| 参数      | 说明           | 类型    | 可选值      | 默认值 |
| --------- | -------------- | ------- | ----------- | ------ |
| animation | 是否动画       | Boolean | false/true  | true   |
| decimals  | 小数点位数     | Number  | —           | 0      |
| span      | 栅格数         | String  | —           | 8      |
| data      | 数据           | Array   | —           | -      |

[DataTabs 数据展示](https://v2.avuejs.com/data/data1/)