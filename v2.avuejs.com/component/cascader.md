cascader级联选择器
=============

值: [ "zhinan", "shejiyuanze", "yizhi" ]  
返回单节点: zhinan  
仅显示最后一级值: [ "zhinan", "shejiyuanze", "yizhi" ]  
多选: [ [ "zhinan", "shejiyuanze", "yizhi" ] ]  
选择任意一级选项: [ "zhinan", "shejiyuanze", "yizhi" ]  
懒加载值: [ "110000", "110100", "110101" ]  

```vue
<el-row :span="24">
  <el-col :span="6">
    值:{{form}}<br/>
    <avue-cascader v-model="form" :dic="dic"></avue-cascader>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    返回单节点:{{form3}}<br/>
    <avue-cascader :emit-path="false" check-strictly v-model="form3" :dic="dic"></avue-cascader>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    仅显示最后一级值:{{form}}<br/>
    <avue-cascader v-model="form" :show-all-levels="false" :dic="dic"></avue-cascader>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    多选:{{form2}}<br/>
    <avue-cascader v-model="form2" multiple :dic="dic"></avue-cascader>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    选择任意一级选项:{{form}}<br/>
    <avue-cascader v-model="form" check-strictly :dic="dic"></avue-cascader>
  </el-col>
  <el-col :span="24"></el-col>
  <el-col :span="6">
    懒加载值:{{form1}}<br/>
    <avue-cascader lazy :lazy-load="lazyLoad" :props="props" v-model="form1"></avue-cascader>
  </el-col>
</el-row>

<script>
export default {
  data() {
    return {
      form: [ "zhinan", "shejiyuanze", "yizhi" ],
      form1: [ "110000", "110100", "110101" ],
      form2: [ [ "zhinan", "shejiyuanze", "yizhi" ]],
      form3: 'zhinan',
      props: {
        label: 'name',
        value: 'code'
      },
      dic: [
        {
          value: 'zhinan',
          label: '指南',
          children: [
            {
              value: 'shejiyuanze',
              label: '设计原则',
              children: [
                { value: 'yizhi', label: '一致' },
                { value: 'fankui', label: '反馈' }
              ]
            }
          ]
        }
      ]
    }
  },
  methods: {
    lazyLoad(node, resolve) {
      let baseUrl = 'https://cli.avuejs.com/api/area';
      let stop_level = 2;
      let level = node.level;
      let data = node.data || {};
      let code = data.code;
      let list = [];
      let callback = () => {
        resolve((list || []).map(ele => {
          return Object.assign(ele, { leaf: level >= stop_level });
        }));
      };
      if (level == 0) {
        axios.get(`${baseUrl}/getProvince`).then(res => {
          list = res.data.data;
          callback();
        });
      } else if (level == 1) {
        axios.get(`${baseUrl}/getCity/${code}`).then(res => {
          list = res.data.data;
          callback();
        });
      } else if (level == 2) {
        axios.get(`${baseUrl}/getArea/${code}`).then(res => {
          list = res.data.data;
          callback();
        });
      } else {
        callback();
      }
    }
  }
}
</script>

[slider滑动框](https://v2.avuejs.com/component/slider/) [upload 附件上传](https://v2.avuejs.com/component/upload/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号