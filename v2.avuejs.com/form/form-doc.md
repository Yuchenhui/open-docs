Form属性文档
========

//2.12.1+支持
//form组件全局配置
app.use(Avue,{
  formOption:{}
})

//可以获取到el-form的内置ref对象
this.$refs.form.$refs.form

Form

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| value/v-model | 绑定值 | object | - | - |
| option | 表单配置项参考Option配置 | object | - | - |
| upload-before | upload组件上传前的回调,done用于继续图片上传，loading用于中断操作 | function | - | (file,done,loading)=>{} |
| upload-after | upload组件上传后的回调,done用于结束操作，loading用于中断操作 | function | - | (res,done)=>{} |
| upload-delete | upload组件删除文件之前的钩子，参数为上传的文件和文件列表，若返回 false 或者返回 Promise 且被 reject，则停止删除 | function | - | (file,column)=>{} |
| upload-preview | upload组件查看回调 | function | - | (file,column,done)=>{} |
| upload-error | upload组件上传失败错误回调 | function | - | (error,column)=>{} |
| upload-exceed | upload组件上传超过长度限制回调 | function | - | (limit,files,fileList,column)=>{} |

Option

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| size | 组件的尺寸 | number | medium/small/mini | small |
| column | 表单列配置参考Column相关配置 | array | - | - |
| labelWidth | 标题宽度 | string | - | 80 |
| labelPosition | 标题位置 | string | left/right/top | left |
| labelSuffix | 标题的后缀 | string | - | : |
| enter | 回车按键触发提交表单 | boolean | - | false |
| group | 分组表单 | array | - | - |
| tabs | 选项卡表单(前提要配置group) | boolean | - | false |
| menuBtn | 表单操作栏是否显示 | boolean | - | true |
| menuSpan | 表单操作菜单栅格占据的列数 | number | - | 24 |
| menuPosition | 表单操作菜单的位置 | string | left/center/right | center |
| submitBtn | 提交按钮 | boolean | - | true |
| submitText | 提交按钮文案 | string | - | 提交 |
| emptyBtn | 清空按钮 | boolean | - | true |
| emptyText | 清空按钮文案 | string | - | 清空 |

Column-共用属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| label | 标签文本的内容 | string | — | — |
| prop | 标签文本的内容属性名称 | string | — | - |
| control | 字段控制器 | function/ promise2.13.0 | — | - |
| bind | 深结构数据绑定值 | string | — | - |
| rules | 验证规则 | object | — | - |
| value | 初始化默认值 | - | - | - |
| disabled | 禁用 | boolean | — | false |
| order | 位置排序，数字越大位置越靠前 | number | — | - |
| size | 组件的尺寸 | number | medium/small/mini | small |
| span | 栅格占据的列数 | number | - | 12 |
| gutter | 栅格间隔 | number | - | 0 |
| offset | 栅格左侧的间隔格数 | number | - | 0 |
| push | 栅格向右移动格数 | number | - | 0 |
| pull | 栅格向左移动格数 | number | - | 0 |
| row | 栅格后面的内容是否从新的一行开始展示 | boolean | - | false |
| display | 栅格显示 | boolean | - | true |
| separator | 选项分隔符,dataType为string时生效 | string | - | , |
| labelWidth | 标题宽度 | string | - | 80 |
| labelPosition | 标题位置 | string | left/right/top | left |
| tip | 内容提示辅助语 | string | - | - |
| tipPlacement | 内容提示辅助语位置 | string | top/top-start/top-end/bottom/bottom-start/bottom-end/left/left-start/left-end/right/right-start/right-end | top |
| labelTip | 标题提示辅助语 | string | - | - |
| labelTipPlacement | 标题提示辅助语位置 | string | top/top-start/top-end/bottom/bottom-start/bottom-end/left/left-start/left-end/right/right-start/right-end | top |

Column-字典属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| props | 数据字典属性的配置对象，具体参考Props参考配置 | object | — | — |
| dicData | 数据字典值 | array/(function/promise)2.13.0 | — | — |
| dicUrl | 数据字典接口url地址 | string | — | — |
| dicQuery | 数据字典接口url携带请求参数 | object | — | — |
| dicHeaders | 数据字典接口url携带头部参数 | object | — | — |
| dicFormatter | 数据字典接口url返回数据格式化方法 | function | — | (res)=>{return res} |
| dicMethod | 数据字典接口请求方式 | string | — | — |

Column-Props

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| label | 选项标签为选项对象的某个属性值 | string | — | label |
| value | 选项的值为选项对象的某个属性值 | string | — | value |
| children | 选项的子选项为选项对象的某个属性值 | string | — | children |
| disabled | 选项的禁用为选项对象的某个属性值 | string | — | disabled |
| res | 选项返回结构的层级(例如data.data) | string | — | - |

Column-Input

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| placeholder | 输入框占位文本 | string | - | 请输入/请选择+label名称 |
| clearable | 是否可清空 | boolean | - | true |
| readonly | 是否只读 | boolean | - | - |
| blur | 在失去焦点时触发 | function | - | ({column,value})=>{} |
| focus | 在获得焦点时触发 | function | - | ({column,value})=>{} |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| maxlength | 原生属性，最大输入长度 | number | - | - |
| minlength | 原生属性，最小输入长度 | number | - | - |
| prepend | 头部文本 | string | - | - |
| append | 尾部文本 | string | - | - |
| prependClick | 头部文本点击事件 | Function | - | - |
| appendClick | 尾部文本点击事件 | Function | - | - |
| prefixIcon | 输入框头部图标 | string | - | - |
| suffixIcon | 输入框尾部图标 | number | - | - |
| showPassword | 是否显示切换密码图标 | boolean | - | true |
| rows | 输入框行数，只对 type="textarea" 有效 | number | - | 2 |
| minRows | 输入框行最小行数，只对 type="textarea" 有效 | number | - | 2 |
| maxRows | 输入框行最大行数，只对 type="textarea" 有效 | number | - | 6 |

Column-Number

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| placeholder | 输入框占位文本 | string | - | 请输入/请选择+label名称 |
| clearable | 是否可清空 | boolean | - | true |
| readonly | 是否只读 | boolean | - | - |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| precision | 精度 | number | - | 2 |
| min | 设置计数器允许的最小值 | number | - | -Infinity |
| max | 设置计数器允许的最大值 | number | - | Infinity |
| step | 计数器步长 | number | - | 1 |
| controls | 是否使用控制按钮 | boolean | true/false | true |
| controlsPosition | 控制按钮位置 | string | right/top | top |

Column-Select

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| placeholder | 输入框占位文本 | string | - | 请输入/请选择+label名称 |
| clearable | 是否可清空 | boolean | - | true |
| readonly | 是否只读 | boolean | - | - |
| blur | 在失去焦点时触发 | function | - | ({column,value})=>{} |
| focus | 在获得焦点时触发 | function | - | ({column,value})=>{} |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| cascader | 级联的子节点prop | array | - | - |
| cascaderIndex | 级联的默认选项序号 | number | - | - |
| multiple | 多选 | boolean | true/false | false |
| limit | 最大允许选择个数 | number | - | - |
| tags | 多选时是否将选中值按文字的形式展示 | boolean | true/false | false |
| allowCreate | 是否允许用户创建新条目，需配合 filterable 使用 | boolean | true/false | false |
| filterable | 是否可搜索 | boolean | true/false | false |
| remote | 是否为远程搜索 | boolean | true/false | false |
| defaultFirstOption | 在输入框按下回车，选择第一个匹配项。需配合 filterable 或 remote 使用 | boolean | true/false | false |
| loadingText | 远程加载时显示的文字 | string | - | 加载中 |
| popperClass | 下拉框的类名 | string | - | - |
| popperAppendToBody | 是否将弹出框插入至 body 元素。在弹出框的定位出现问题时，可将该属性设置为 false | boolean | - | true |

Column-Cascader

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| placeholder | 输入框占位文本 | string | - | 请输入/请选择+label名称 |
| clearable | 是否可清空 | boolean | - | true |
| readonly | 是否只读 | boolean | - | - |
| blur | 在失去焦点时触发 | function | - | ({column,value})=>{} |
| focus | 在获得焦点时触发 | function | - | ({column,value})=>{} |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| showAllLevels | 级联输入框中是否显示选中值的完整路径 | boolean | true/false | true |
| tags | 多选时是否将选中值按文字的形式展示 | boolean | true/false | false |
| separator | 选项分隔符 | string | - | - |
| filterable | 是否可搜索选项 | boolean | true/false | false |
| filterMethod | 自定义搜索逻辑，第一个参数是节点node，第二个参数是搜索关键词keyword，通过返回布尔值表示是否命中 | function | - | - |
| expandTrigger | 次级菜单的展开方式 | string | click/hover | hover |
| multiple | 是否多选 | boolean | true/false | false |
| checkStrictly | 是否严格的遵守父子节点不互相关联 | boolean | true/false | false |
| emitPath | 在选中节点改变时，是否返回由该节点所在的各级菜单的值所组成的数组，若设置false，则只返回该节点的值 | boolean | true/false | true |
| lazy | 是否动态加载子节点，需与 lazyLoad 方法结合使用 | boolean | true/false | false |
| lazyLoad | 加载动态数据的方法，仅在 lazy 为 true 时有效 function(node, resolve)，node为当前点击的节点，resolve为数据加载完成的回调(必须调用) | function | - | - |
| popperClass | 下拉框的类名 | string | - | - |

Column-Checkbox

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| readonly | 是否只读 | boolean | - | - |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| all | 是否启动全选 | boolean | true/false | - |
| border | 是否显示边框 | boolean | true/false | - |
| min | 可被勾选的 checkbox 的最小数量 | number | - | - |
| max | 可被勾选的 checkbox 的最大数量 | number | - | - |

Column-Radio

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| readonly | 是否只读 | boolean | - | - |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| border | 显示边框 | boolean | true/false | false |
| button | 按钮组类型 | boolean | true/false | false |

Column-Date

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| placeholder | 输入框占位文本 | string | - | 请输入/请选择+label名称 |
| clearable | 是否可清空 | boolean | - | true |
| readonly | 是否只读 | boolean | - | - |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| startPlaceholder | 日期/时间范围开始占位符 | string | - | 开始 |
| endPlaceholder | 日期/时间范围结束占位符 | string | - | 结束 |
| rangeSeparator | 选择范围时的分隔符 | string | - | - |
| valueFormat | 真实值的时间格式 | string | - | - |
| format | 显示值时间格式 | string | - | - |
| defaultTime | 范围选择时选中日期所使用的当日内具体时刻 | string[] | 数组，长度为 2，每项值为字符串，形如12:00:00，第一项指定开始日期的时刻，第二项指定结束日期的时刻，不指定会使用时刻 00:00:00 | - |
| defaultValue | 可选，选择器打开时默认显示的时间 | Date | - | - |
| pickerOptions | 当前时间日期选择器特有的选项 | object | - | - |
| popperClass | 下拉框的类名 | string | - | - |

Column-Time

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| placeholder | 输入框占位文本 | string | - | 请输入/请选择+label名称 |
| clearable | 是否可清空 | boolean | - | true |
| readonly | 是否只读 | boolean | - | - |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| startPlaceholder | 日期/时间范围开始占位符 | string | - | 开始 |
| endPlaceholder | 日期/时间范围结束占位符 | string | - | 结束 |
| rangeSeparator | 选择范围时的分隔符 | string | - | - |
| valueFormat | 真实值的时间格式 | string | - | - |
| format | 显示值时间格式 | string | - | - |
| defaultValue | 可选，选择器打开时默认显示的时间 | Date | - | - |
| pickerOptions | 当前时间日期选择器特有的选项 | object | - | - |
| popperClass | 下拉框的类名 | string | - | - |

Column-Switch

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| len | 滑块的宽度 | number | - | 40 |
| activeIconClass | 打开时所显示图标的类名，设置此项会忽略active-text | string | - | - |
| inactiveIconClass | 关闭时所显示图标的类名，设置此项会忽略 inactive-text | string | - | - |
| activeColor | 打开时的背景色 | string | - | #409EFF |
| inactiveColor | 关闭时的背景色 | string | - | #C0CCDA |

Column-Upload

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| accept | upload时文件类型 | string/array | - | - |
| fileSize | 上传文件的大小限制，单位为KB,超出大小回调upload-error函数进行操作 | number | - | - |
| action | 必选参数，上传的地址 | string | - | - |
| propsHttp | 返回数据结构体propsHttp配置 | object | - | - |
| data | 携带的附加参数 | object | - | - |
| headers | 携带的头部附加参数 | object | - | - |
| limit | 最大允许上传个数 | number | - | - |
| fileType | 如果没后缀，用来指定文件类型 | string | - | img/audio/video |
| fileText | 按钮上传文案 | string | 点击上传 | - |
| listType | 文件列表的类型 | string | text/picture/picture-card | text |
| showFileList | 是否显示已上传文件列表 | boolean | true/false | true |
| multiple | 是否支持多选文件 | boolean | true/false | false |
| canvasOption | 图片水印canvasOption配置 | object | - | - |

Column-propsHttp

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| home | 图片的根路径地址，例如返回data:{url:' / xxxx.jpg',name:''},home属性为http://xxx.com/,则最终的图片显示地址为http://xxx.com/xxxx.jpg | string | - | - |
| res | 返回结构体的层次，例如返回data:{url:'',name:''},则res配置为data | string | - | - |
| url | 上传成功返回结构体的图片地址，例如返回data:{urlsrc:'',name:''},则url配置为urlsrc | string | - | - |
| name | 上传成功返回结构体的图片名称，例如返回data:{urlsrc:'',namesrc:''},则name配置为namesrc，当listType为picture-img属性不存在 | string | - | - |
| fileName | 上传文件流时的名称 | string | - | file |

Column-canvasOption

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| text | 字体的文字 | string | - | avuejs.com |
| fontFamily | 字体类型 | string | - | microsoft yahei |
| color | 字体的颜色 | string | - | #999 |
| fontSize | 字体的大小 | string | - | 16 |
| opacity | 文字的透明度 | string | - | 100 |
| bottom | 文字距离图片底部的距离 | string | - | 10 |
| right | 文字距离图片右边的距离 | string | - | 10 |
| ratio | 压缩图片比率0-1(可以是小数) | number | - | 1 |

Column-Array/Url

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| alone | 单个模式 | boolean | true/false | false |
| limit | 最大框的个数 | number | - | - |

Column-Img

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| alone | 单个模式 | boolean | true/false | false |
| limit | 最大框的个数 | number | - | - |
| fileType | 如果没后缀，用来指定文件类型 | string | - | img/audio/video |

Column-Dynamic

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| rowAdd | 新增方法 | function | - | - |
| rowDel | 删除方法 | function | - | - |
| type | 展示类型 | string | form/crud | crud |
| limit | 限制当前最大行数 | number | - | - |

Column-Tree

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| placeholder | 输入框占位文本 | string | - | 请输入/请选择+label名称 |
| clearable | 是否可清空 | boolean | - | true |
| readonly | 是否只读 | boolean | - | - |
| blur | 在失去焦点时触发 | function | - | ({column,value})=>{} |
| focus | 在获得焦点时触发 | function | - | ({column,value})=>{} |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| multiple | 多选 | boolean | true/false | false |
| tags | 多选时是否将选中值按文字的形式展示 | boolean | true/false | false |
| checkStrictly | 在显示复选框的情况下，是否严格的遵循父子不互相关联的做法 | boolean | true/false | false |
| parent | 是否可以选择父类 | boolean | true/false | true |
| accordion | 是否每次只打开一个同级树节点展开 | boolean | true/false | false |
| defaultExpandAll | 是否默认展开所有节点 | boolean | true/false | false |
| expandOnClickNode | 是否在点击节点的时候展开或者收缩节点,如果为 false，则只有点箭头图标的时候才会展开或者收缩节点 | boolean | true/false | false |
| defaultExpandedKeys | 默认展开的节点的 key 的数组 | array | - | - |
| defaultCheckedKeys | 默认勾选的节点的 key 的数组 | array | - | - |
| filters | 是否开启条件筛选 | boolean | true/false | true |
| filterText | 条件筛选提示语 | string | - | 请输入搜索关键字 |
| iconClass | 自定义树节点的图标 | string | - | - |
| leafOnly | 子类全选时勾选值不包含父类 | boolean | true/false | false |
| parent | 父类是否可以点击和选择 | boolean | true/false | true |
| lazy | 是否懒加载子节点，需与 load 方法结合使用 | boolean | true/false | false |
| treeLoad | 加载子树数据的方法，仅当 lazy 属性为true 时生效 | function | - | - |
| nodeClick | 节点被点击时的回调,共三个参数，依次为：传递给 data 属性的数组中该节点所对应的对象、节点对应的 Node、节点组件本身。 | function | - | - |
| checked | 当复选框被点击的时候触发共,两个参数，依次为：传递给 data 属性的数组中该节点所对应的对象、树目前的选中状态对象 | function | - | - |
| popperClass | 下拉框的类名 | string | - | - |
| popperAppendToBody | 是否将弹出框插入至 body 元素。在弹出框的定位出现问题时，可将该属性设置为 false | boolean | - | true |

Column-Table

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| formatter | 展示数据格式化 | function | - | - |
| onLoad | 首次加载数据、查询、翻页方法 | function | - | - |
| before-close2.12.7 | 关闭前的回调，会暂停Dialog的关闭，done用于关闭Dialog | function | - | (done)=>{} |

Column-Icon

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| iconList | 图标数组 | array | - | - |
| before-close2.12.7 | 关闭前的回调，会暂停Dialog的关闭，done用于关闭Dialog | function | - | (done)=>{} |

Column-Map

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| params | 高德地图的初始化参数 | object | - | - |
| before-close2.12.7 | 关闭前的回调，会暂停Dialog的关闭，done用于关闭Dialog | function | - | (done)=>{} |

Column-Color

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| showAlpha | 是否支持透明度选择 | boolean | - | true |
| colorFormat | 颜色的格式 | string | hsl/hsv/hex/rgb | rgb |
| popperClass | 下拉框的类名 | string | - | - |
| predefine | 预定义颜色 | array | - | - |

Column-Slider

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| min | 最小值 | number | - | 0 |
| max | 最大值 | number | - | 100 |
| showInput | 是否显示输入框，仅在非范围选择时有效 | boolean | - | false |
| showInputControls | 在显示输入框的情况下，是否显示输入框的控制按钮 | boolean | - | true |
| vertical | 是否竖向模式 | boolean | - | false |
| height | Slider 高度，竖向模式时必填 | string | - | - |
| step | 步长 | number | - | 1 |
| range | 是否为范围选择 | boolean | true/false | false |
| showInput | 是否显示输入框，仅在非范围选择时有效 | boolean | true/false | false |
| showStops | 是否显示间断点 | boolean | true/false | false |
| showTooltip | 是否显示 tooltip | boolean | true/false | true |
| formatTooltip | 格式化 tooltip message | function | true/false | - |
| tooltipClass | tooltip 的自定义类名 | string | - | - |
| marks | 标记， key 的类型必须为 number 且取值在闭区间 [min, max] 内，每个标记可以单独设置样式 | object | - | - |

Column-Rate

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| change | 值改变的时触发 | function | - | ({column,value})=>{} |
| click | 点击时触发 | boolean | - | ({column,value})=>{} |
| max | 最大分值 | number | - | 5 |
| allowHalf | 是否允许半选 | boolean | - | false |
| lowThreshold | 低分和中等分数的界限值，值本身被划分在低分中 | number | - | 2 |
| highThreshold | 高分和中等分数的界限值，值本身被划分在高分中 | number | - | 4 |
| colors | icon 的颜色。若传入数组，共有 3 个元素，为 3 个分段所对应的颜色；若传入对象，可自定义分段，键名为分段的界限值，键值为对应的颜色 | array/object | - | ['#F7BA2A', '#F7BA2A', '#F7BA2A'] |
| voidColor | 未选中 icon 的颜色 | string | - | #C6D1DE |
| disabledVoidColor | 只读时未选中 icon 的颜色 | string | - | #EFF2F7 |
| iconClasses | icon 的类名。若传入数组，共有 3 个元素，为 3 个分段所对应的类名；若传入对象，可自定义分段，键名为分段的界限值，键值为对应的类名 | array/object | - | ['el-icon-star-on', 'el-icon-star-on','el-icon-star-on'] |
| voidIconClass | 未选中 icon 的类名 | string | - | el-icon-star-off |
| disabledVoidIconClass | 只读时未选中 icon 的类名 | string | - | el-icon-star-on |
| showText | 是否显示辅助文字，若为真，则会从 texts 数组中选取当前分数对应的文字内容 | boolean | - | false |
| showScore | 是否显示当前分数，show-score 和 show-text 不能同时为真 | boolean | - | false |
| textColor | 辅助文字的颜色 | string | - | #1F2D3D |
| texts | 辅助文字数组 | array | - | ['极差', '失望', '一般', '满意', '惊喜'] |
| scoreTemplate | 分数显示模板 | boolean | - | {value} |

Events

| 事件名称 | 说明 | 参数 |
| --- | --- | --- |
| submit | 表单提交回调事件 | form,done |
| reset-change | 表单清空回调事件 | - |

Methods

| 事件名称 | 说明 | 参数 |
| --- | --- | --- |
| submit | 对整个表单进行提交 | - |
| resetForm | 对整个表单进行重置 | - |
| updateDic | 更新指定字典 | prop,dic |
| dicInit | 重新加载全部字典 | - |
| getPropRef | 获取prop的ref对象 | prop |
| validate | 对整个表单进行校验的方法，参数为一个回调函数。该回调函数会在校验结束后被调用，并传入两个参数：是否校验成功和未通过校验的字段。若不传入回调函数，则会返回一个 promise (callback: Function(boolean, object)) | - |
| validateField | 对部分表单字段进行校验的方法 | Function(props: array / string, callback: Function(errorMessage: string)) |
| resetFields | 对整个表单进行重置，将所有字段值重置为初始值并移除校验结果 | - |
| clearValidate | 移除表单项的校验结果。传入待移除的表单项的 prop 属性或者 prop 组成的数组，如不传则移除整个表单的校验结果 | Function(props: array / string) |

Slot

| 名称 | 说明 |
| --- | --- |
| 'prop' | 表单 |
| 'prop'Label | 表单的标题 |
| 'prop'Error | 表单错误提示 |
| menuForm | 菜单 |
| menuFormBefore | 菜单前 |

[Input输入框](https://v2.avuejs.com/form/form-input/)

Install Cancel

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号