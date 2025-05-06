Notice 消息通知
===========

Tips

2.2.0+

    <el-tabs v-model="activeName">
      <el-tab-pane label="邮件(1)" name="first"></el-tab-pane>
      <el-tab-pane label="消息(2)" name="second"></el-tab-pane>
      <el-tab-pane label="通知" name="third"></el-tab-pane>
      <el-tab-pane label="计划" name="fourth"></el-tab-pane>
    </el-tabs>
    <avue-notice @click="handleClick" :data="data" :option="option" @page-change="pageChange"></avue-notice>
    <script>
    let list = [
      {
        img: 'https://avuejs.com/images/logo-bg.jpg',
        title: '史蒂夫·乔布斯 关注了你',
        subtitle: '05-08 15:08',
        tag: '已经开始',
        status: 0
      },
      {
        img: 'https://avuejs.com/images/logo-bg.jpg',
        title: '斯蒂夫·沃兹尼亚克 关注了你',
        subtitle: '05-08 15:08',
        tag: '未开始',
        status: 1
      },
      {
        img: 'https://avuejs.com/images/logo-bg.jpg',
        title: '乔纳森·伊夫 关注了你',
        subtitle: '05-08 15:08',
        tag: '有警告',
        status: 2
      },
      {
        img: 'https://avuejs.com/images/logo-bg.jpg',
        title: '蒂姆·库克 关注了你',
        subtitle: '05-08 15:08',
        status: 3,
        tag: '有错误'
      },
      {
        img: 'https://avuejs.com/images/logo-bg.jpg',
        title: '比尔·费尔南德斯 关注了你',
        subtitle: '05-08 15:08',
        status: 4,
        tag: '已完成'
      }
    ]
    export default {
      data() {
        return {
          activeName: 'first',
          option: {
            props: {
              img: 'img',
              title: 'title',
              subtitle: 'subtitle',
              tag: 'tag',
              status: 'status'
            },
          },
          data: list,
        }
      },
      methods: {
        handleClick(item) {
          this.$message.success(JSON.stringify(item))
        },
        pageChange(page, done) {
          setTimeout(() => {
            this.$message.success('页码' + page)
            this.data = this.data.concat(list);
            done();
          }, 1000)
        },
      }
    }
    </script>