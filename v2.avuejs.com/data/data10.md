DataImgtext 数据展示
================
  
<avue-data-imgtext :option="option"></avue-data-imgtext>
<script>
export default {
  data(){
    return {
      option: {
        span: 8,
        data: [
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '网易掌门人',
            imgsrc: '/images/card2.jpg',
            headimg: [
              {
                src: '/images/card1.jpg',
                name: '张三'
              },
              {
                src: '/images/card2.jpg',
                name: '李四'
              },
              {
                src: '/images/card3.jpg',
                name: '王五'
              },
            ],
            content: 'xxxxx',
            href: 'https://avuejs.com',
            target: '_blank',
            time: '刚刚'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '小马',
            imgsrc: '/images/card1.jpg',
            headimg: [
              {
                src: '/images/card1.jpg',
                name: '张三'
              },
              {
                src: '/images/card2.jpg',
                name: '李四'
              },
              {
                src: '/images/card3.jpg',
                name: '王五'
              },
            ],
            content: 'xxxxxx',
            href: 'https://avuejs.com',
            target: '_blank',
            time: '几秒前'
          },
          {
            click: function (item) {
              alert(JSON.stringify(item));
            },
            title: '桐人',
            imgsrc: '/images/card3.jpg',
            headimg: [
              {
                src: '/images/card1.jpg',
                name: '张三'
              },
              {
                src: '/images/card2.jpg',
                name: '李四'
              },
              {
                src: '/images/card3.jpg',
                name: '王五'
              },
            ],
            content: 'xxxxxxxx',
            href: 'https://avuejs.com',
            target: '_blank',
            time: '一小时前'
          },
        ]
      },
    }
  }
}
</script>