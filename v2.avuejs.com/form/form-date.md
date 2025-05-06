Date日期
======

基础用法
-------------------------------------------------------------------------------------

基本单位由type属性指定。快捷选项需配置`pickerOptions`对象中的`shortcuts`，禁用日期通过 `disabledDate` 设置，传入函数

```vue
<avue-form v-model="form" :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        form:{},
        option:{
          column: [{
              label: "日期",
              prop: "datetime",
              type: "datetime",
          }, {
              label: "快捷方式",
              prop: "date",
              type: "date",  
              pickerOptions: {
              shortcuts: [{
                text: '今天',
                onClick(picker) {
                  picker.$emit('pick', new Date());
                }
              }, {
                text: '昨天',
                onClick(picker) {
                  const date = new Date();
                  date.setTime(date.getTime() - 3600 * 1000 * 24);
                  picker.$emit('pick', date);
                }
              }, {
                text: '一周前',
                onClick(picker) {
                  const date = new Date();
                  date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
                  picker.$emit('pick', date);
                }
              }]
            }
          }, {
              label: "禁止日期",
              prop: "date",
              type: "date",  
              pickerOptions: {
              disabledDate(time) {
                return time.getTime() < Date.now();
              },
            }
          }]
        },
      };
    }
}
</script>
```

日期格式化
-------------------------------------------------------------------------------------

请注意大小写

| 格式         | 含义          | 备注                         | 举例           |
| ------------ | ------------- | ----------------------------| -------------- |
| `yyyy`       | 年            |                              | 2017           |
| `M`          | 月            | 不补0                       | 1              |
| `MM`         | 月            |                             | 01             |
| `W`          | 周            | 仅周选择器的`format`可用；不补0 | 1              |
| `WW`         | 周            | 仅周选择器的`format`可用    | 01             |
| `d`          | 日            | 不补0                       | 2              |
| `dd`         | 日            |                             | 02             |
| `H`          | 小时          | 24小时制；不补0              | 3              |
| `HH`         | 小时          | 24小时制                    | 03             |
| `h`          | 小时          | 12小时制，须和`A`或`a`使用；不补0 | 3              |
| `hh`         | 小时          | 12小时制，须和`A`或`a`使用   | 03             |
| `m`          | 分钟          | 不补0                       | 4              |
| `mm`         | 分钟          |                             | 04             |
| `s`          | 秒            | 不补0                       | 5              |
| `ss`         | 秒            |                             | 05             |
| `A`          | AM/PM         | 仅`format`可用，大写        | AM             |
| `a`          | am/pm         | 仅`format`可用，小写        | am             |
| `timestamp`  | JS时间戳      | 仅`value-format`可用；组件绑定值为`number`类型 | 1483326245000  |

格式化
---------------------------------------------------------------------------

使用`format`指定输入框的格式；使用`valueFormat`指定绑定值的格式。

```vue
<avue-form v-model="form" :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        form:{},
        option:{
          column: [{
              label: "日期",
              prop: "datetime",
              type: "datetime",
              format:'yyyy年MM月dd日 HH时mm分ss秒',
              valueFormat:'yyyy-MM-dd HH:mm:ss'
          }, {
              label: "时间戳",
              prop: "datetime",
              type: "datetime",
              format: "yyyy-MM-dd hh:mm:ss",
              valueFormat: "timestamp",
          }]
        },
      };
    }
}
</script>
```

其他日期单位
---------------------------------------------------------------------------------------------------------

```vue
<avue-form v-model="form" :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        form:{},
        option:{
          labelWidth:110,
          column: [ {
              label: "时间",
              prop: "time",
              type: "time",
              format:'HH:mm:ss',
              valueFormat:'HH:mm:ss',
          }, {
              label: "周",
              prop: "week",
              type: "week",
              format: "yyyy 第 WW 周"
          }, {
              label: "月",
              prop: "month",
              type: "month",
          },{
              label: "月范围",
              prop: "monthrange",
              type: "monthrange",
              format:'yyyy-MM',
              valueFormat:'yyyy-MM'
          }, {
              label: "年",
              prop: "year",
              type: "year",
          }, {
              label: "多个日期",
              prop: "dates",
              type: "dates",
              format: "yyyy-MM-dd",
              valueFormat: "yyyy-MM-dd",
          }]
        },
      };
    }
}
</script>
```

日期范围
-------------------------------------------------------------------------------------

```vue
<avue-form v-model="form" :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        form:{
            datetime:'1398250549123'//时间戳例子
        },
        option:{
          labelWidth:110,
          column: [{
              label: "时间日期范围",
              type: 'datetimerange',
              prop:'datetimerange',
              format:'yyyy-MM-dd HH:mm:ss',
              valueFormat:'yyyy-MM-dd HH:mm:ss',
              startPlaceholder: '时间日期开始范围自定义',
              endPlaceholder: '时间日期结束范围自定义',
          },{
              label: "日期范围",
              prop: "daterange",
              type: "daterange",
              format:'yyyy-MM-dd',
              valueFormat:'yyyy-MM-dd',
              startPlaceholder: '日期开始范围自定义',
              endPlaceholder: '日期结束范围自定义',
          }]
        },
      };
    }
}
</script>
```

下拉框样式
-----------------------------------------------------------------------------------------------

```css
.popperClass .available{
  background-color: rgba(0,0,0,.2);
}
```

`popperClass`属性配置样式的`class`名字

```vue
<avue-form v-model="form" :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        form:{},
        option:{
          column: [{
              label: "日期",
              prop: "datetime",
              popperClass:'popperClass',
              type: "datetime",
          }]
        }
      }
    }
}
</script>
```

默认的起始与结束时刻
-------------------------------------------------------------------------------------------------------------------------------------------------

使用`datetimerange`进行范围选择时，在日期选择面板中选定起始与结束的日期，默认会使用该日期的`00:00:00`作为起始与结束的时刻；通过选项`defaultTime`可以控制选中起始与结束日期时所使用的具体时刻。`defaultTime`接受一个数组，数组每项值为字符串，形如`12:00:00`，其中第一项控制起始日期的具体时刻，第二项控制结束日期的具体时刻。

```vue
<avue-form v-model="form" :option="option"></avue-form>

<script>
export default {
    data() {
      return {
        form:{
            datetime:'1398250549123'//时间戳例子
        },
        option:{
          labelWidth:110,
          column: [{
              label: "时间日期范围",
              type: 'datetimerange',
              prop:'datetimerange',
              span:24,
              defaultTime:['12:00:00', '08:00:00'],
              format:'yyyy-MM-dd HH:mm:ss',
              valueFormat:'yyyy-MM-dd HH:mm:ss',
              startPlaceholder: '时间日期开始范围自定义',
              endPlaceholder: '时间日期结束范围自定义',
          }]
        },
      };
    }
}
</script>
```

[Radio单选框](https://v2.avuejs.com/form/form-radio/) [Time时间](https://v2.avuejs.com/form/form-time/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号