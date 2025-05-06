Flow 流程
=======

常用的流程组件

Tips

2.0.4

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里-->
<script src="https://cdn.staticfile.net/jsPlumb/2.11.1/js/jsplumb.min.js"></script>
<el-button type="primary" @click="$refs.flow.addNode('测试节点')">添加节点</el-button>
<el-button type="primary" @click="handleNext">下一个节点</el-button>
<br /><br />
<avue-flow :height="600" :width="1200" ref="flow" :option="option" v-model="form">
  <template slot-scope="scope" slot="header">
    <i class="el-icon-delete" @click="$refs.flow.deleteNode(scope.node.id)"></i>
    自定义头部
  </template>
  <div slot-scope="{node}">
    <span>自定义{{(node || {}).name}}</span>
  </div>
</avue-flow>

<script>
export default {
  data() {
    return {
      count: 0,
      form: '',
      option: {
        "name": "流程A",
        "nodeList": [
          {
            "id": "nodeA",
            "name": "流程A-节点A",
            "left": 39,
            "top": 110
          },
          {
            "id": "nodeB",
            "name": "流程A-节点B",
            "left": 340,
            "top": 161
          },
          {
            "id": "nodeC",
            "name": "流程A-节点C",
            "left": 739,
            "top": 161
          },
          {
            "id": "nodeD",
            "name": "节点D",
            "left": 739,
            "top": 20
          }
        ],
        "lineList": [
          {
            "from": "nodeA",
            "to": "nodeB"
          },
          {
            "from": "nodeB",
            "to": "nodeC"
          },
          {
            "from": "nodeC",
            "to": "nodeD"
          }
        ]
      }
    }
  },
  computed: {
    nodeList() {
      return this.option.nodeList
    }
  },
  mounted() {
    this.form = this.nodeList[this.count].id;
  },
  methods: {
    handleClick(node) {
      this.$message.success(JSON.stringify(node))
    },
    handleNext() {
      this.count++
      if (this.count >= this.nodeList.length) {
        this.count = 0;
      }
      this.form = this.nodeList[this.count].id;
    }
  }
}
</script>
```

Variables
---------

| 参数   | 说明       | 类型   | 可选值 | 默认值 |
| ------ | ---------- | ------ | ------ | ------ |
| width  | 画布宽度   | Number | -      | -      |
| height | 画布高度   | Number | -      | -      |
| option | 属性配置   | Object | -      | -      |

Events
------

| 事件名 | 说明       | 参数  |
| ------ | ---------- | ----- |
| click  | 节点点击事件 | node  |

Methods
-------

| 方法名     | 说明    | 参数 |
| ---------- | ------- | ---- |
| nodeAdd    | 节点新增 | name |
| deleteNode | 节点删除 | id   |