大表哥(宇宙最强表格)
===========

<avue-crud :option="option" :data="data" :page.sync="page" @on-load="onLoad"></avue-crud>
<script>
export default {
    data() {
      return {
        page: {
          pageSize: 20
        },
        option: {
          excelBtn: true,
          border: true,
          index: true,
          expandLevel: 3,
          headerAlign: 'center',
          align: 'center',
          tree: true,
          labelWidth: 100,
          column: [
            {
              width: 130,
              label: '姓名',
              prop: 'name',
              display: false
            },
            {
              label: '性别1',
              prop: 'sex',
              display: false
            },
            {
              label: '自定义图标',
              prop: 'icon',
              type: "icon",
              iconList: [
                {
                  label: '基本图表',
                  list: ['el-icon-time', 'el-icon-bell', 'el-icon-star-on']
                }
              ],
              display: false
            },
            {
              label: '多级表头',
              display: false,
              children: [
                {
                  label: '信息',
                  display: false,
                  children: [
                    {
                      label: '年龄',
                      prop: 'age',
                      display: false
                    },
                    {
                      label: '手机号',
                      prop: 'phone',
                      display: false
                    }
                  ]
                },
                {
                  label: '级别',
                  prop: 'grade',
                  type: 'select',
                  display: false,
                  dicData: [
                    {
                      label: '测试',
                      value: 1
                    }
                  ]
                }
              ]
            },
            {
              label: '测试',
              prop: 'test',
              display: false
            }
          ],
          group: [
            {
              label: '用户信息',
              prop: 'jbxx',
              icon: 'el-icon-edit-outline',
              column: [
                {
                  label: '姓名',
                  prop: 'name'
                },
                {
                  label: '年龄',
                  prop: 'age'
                }
              ]
            },
            {
              label: '其他信息',
              prop: 'jbxxs',
              icon: 'el-icon-edit-outline',
              column: [
                {
                  label: '级别',
                  prop: 'grade',
                  type: 'select',
                  dicData: [
                    {
                      label: '测试',
                      value: 1
                    }
                  ]
                },
                {
                  label: '手机信息',
                  prop: 'phone'
                },
                {
                  label: '自定义图标',
                  prop: 'icon',
                  type: "icon",
                  iconList: [
                    {
                      label: '基本图表',
                      list: ['el-icon-time', 'el-icon-bell', 'el-icon-star-on']
                    }
                  ]
                }
              ]
            }
          ]
        },
        data: [
          {
            id: '1',
            name: '张三',
            age: 14,
            grade: 1,
            phone1: '17547400800',
            phone: '17547400800',
            icon: 'el-icon-time',
            test: 1,
            sex: '男',
            children: [
              {
                id: '2',
                name: '李四',
                age: 20,
                grade: 1,
                sex: '男',
                test: 1,
                phone1: '17547400800',
                phone: '17547400800',
                icon: 'el-icon-bell',
                children: [
                  {
                    id: '3',
                    name: '王五',
                    age: 10,
                    grade: 1,
                    test: 1,
                    sex: '女',
                    icon: 'el-icon-star-on',
                    phone1: '17547400800',
                    phone: '17547400800'
                  }
                ]
              }
            ]
          },
          {
            id: '4',
            name: '王五',
            age: 10,
            grade: 1,
            test: 1,
            sex: '女',
            icon: 'el-icon-star-on',
            phone1: '17547400800',
            phone: '17547400800'
          }
        ]
      }
    },
    methods: {
      onLoad(page) {
        //模拟分页
        this.page.total = 40
      }
    }
}
</script>

[表格错位问题](https://v2.avuejs.com/crud/crud-cw/) [CRUD大数据解决方案](https://v2.avuejs.com/crud/api-crud-big/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本 关注Avue Cloud公众号