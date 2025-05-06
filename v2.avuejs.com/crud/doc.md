Crud属性文档
========

```js
//2.12.1+支持
//crud组件全局配置
app.use(Avue,{
  crudOption:{}
})

//可以获取到el-table的内置ref对象
this.$refs.crud.$refs.table
```

### Crud

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| value/v-model | 绑定值 | object | - | - |
| data | 显示的数据 | array | - | - |
| option | 表单配置项参考Option配置 | object | - | - |
| before-open | 打开前的回调，会暂停Dialog的打开，done用于关闭Dialog,type为当前窗口的类型2.13.1新增loading方法 | function | - | (done,type,loading)=>{} |
| before-close | 关闭前的回调，会暂停Dialog的关闭，done用于关闭Dialog,type为当前窗口的类型 | function | - | (done,type)=>{} |
| permission | 表格多个按钮权限控制，采用函数方式可以精确到行控制 | - | - | - |
| search | 搜索变量(需要sync修饰符) | object | - | - |
| page | 分页变量(需要sync修饰符)参考Page参数 | object | - | - |
| cell-class-name | 单元格的className的回调方法，也可以使用字符串为所有单元格设置一个固定的className | function | - | ({row,column,rowIndex,columnIndex})=>{} |
| cell-style | 单元格的 style 的回调方法，也可以使用一个固定的 Object 为所有单元格设置一样的 Style。 | function | - | ({row,column,rowIndex,columnIndex})=>{} |
| header-cell-class-name | 表头单元格的className的回调方法，也可以使用字符串为所有表头单元格设置一个固定的className | function | - | ({ column, columnIndex, row, rowIndex})=>{} |
| header-row-class-name | 表头行的 className 的回调方法，也可以使用字符串为所有表头行设置一个固定的 className。 | function | - | ({rowIndex})=>{} |
| header-row-style | 表头行的 style 的回调方法，也可以使用一个固定的 Object 为所有表头行设置一样的 Style。 | function | - | ({rowIndex})=>{} |
| header-cell-style | 表头单元格的 style 的回调方法，也可以使用一个固定的 Object 为所有表头单元格设置一样的 Style。 | function | - | ({ column, columnIndex, row, rowIndex})=>{} |
| row-class-name | 行的className的回调方法，也可以使用字符串为所有行设置一个固定的className | function | - | ({row,rowIndex})=>{} |
| row-style | 行的 style 的回调方法，也可以使用一个固定的 Object 为所有行设置一样的 Style。 | function | - | ({row,rowIndex})=>{} |
| span-method | 合并行或列的计算方法 | function | - | ({row,column,rowIndex,columnIndex})=>{} |
| summary-method | 自定义的合计计算方法 | function | - | ({columns,data})=>{} |
| table-loading | 表格等待框的控制 | boolean | - | - |
| upload-before | upload组件上传前的回调,done用于继续图片上传，loading用于中断操作 | function | - | (file,done,loading)=>{} |
| upload-after | upload组件上传后的回调,done用于结束操作，loading用于中断操作 | function | - | (res,done)=>{} |
| upload-delete | upload组件删除文件之前的钩子，参数为上传的文件和文件列表，若返回 false 或者返回 Promise 且被 reject，则停止删除 | function | - | (file,column)=>{} |
| upload-preview | upload组件查看回调 | function | - | (file,column,done)=>{} |
| upload-error | upload组件上传失败错误回调 | function | - | (error,column)=>{} |
| upload-exceed | upload组件上传超过长度限制回调 | function | - | (limit,files,fileList,column)=>{} |

### Page

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| currentPage | 当前页数 | number | - | 1 |
| pageSize | 每页显示条目个数 | number | - | 20 |
| total | 总条目数 | number | - | 0 |
| pagerCount | 页码按钮的数量，当总页数超过该值时会折叠 | number | - | 7 |
| background | 是否为分页按钮添加背景色 | boolean | - | true |
| layout | 组件布局，子组件名用逗号分隔 | string | sizes, prev, pager, next, jumper, ->, total, slot | 'prev, pager, next, jumper, ->, total' |
| pageSizes | 每页显示个数选择器的选项设置 | number[] | - | [10, 20, 30, 40, 50, 100] |

### Option

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| size | 组件的尺寸 | number | medium/small/mini | small |
| column | 表单列配置参考Column相关配置 | array | - | - |
| height | 表格的高度，默认为自动高度。如果设置为auto，会自适应窗口高度，配合calcHeight参数去调节范围 | string | - | - |
| maxHeight | 表格的最大高度 | array | - | - |
| stripe | 是否为斑马纹 | boolean | - | false |
| index | 是否有序号 | boolean | - | false |
| indexWidth | 序号列宽度 | number | - | 50 |
| indexFixed | 序号列是否冻结列，true 表示固定在左侧 | boolean/string | true/left/right | true |
| indexClassName | 序号列的单元格自定义类名 | String | - | - |
| indexLabelClassName | 序号列标题的自定义类名 | String | - | - |
| menu | 是否有操作栏 | boolean | - | true |
| menuWidth | 操作栏宽度 | number | - | 220 |
| menuTitle | 操作栏标题 | string | - | 标题 |
| menuFixed | 操作栏列冻结列，true 表示固定在左侧 | boolean/string | true/left/right | true |
| menuClassName | 操作栏列的单元格自定义类名 | String | - | - |
| menuLabelClassName | 操作栏列标题的自定义类名 | String | - | - |
| menuType | 操作栏按钮样式 | string | button/icon/text/menu | text |
| menuHeaderAlign | 操作栏表头的对齐方式 | string | left/center/right | center |
| menuAlign | 操作栏按钮的对齐方式 | string | left/center/right | center |
| selection | 是否有选择框 | boolean | - | false |
| selectable | selection为true，控制返回值用来决定这一行的 CheckBox 是否可以勾选 | function | - | - |
| selectionWidth | 选择框列宽度 | number | - | 50 |
| selectionFixed | 选择框列是否冻结列，true 表示固定在左侧 | boolean/string | true/left/right | true |
| selectionClassName | 选择框列的单元格自定义类名 | String | - | - |
| selectionLabelClassName | 选择框列标题的自定义类名 | String | - | - |
| expand | 是否有展开表格 | boolean | - | false |
| expandWidth | 展开列宽度 | number | - | 50 |
| expandFixed | 展开列是否冻结列，true 表示固定在左侧 | boolean/string | true/left/right | true |
| expandClassName | 展开列的单元格自定义类名 | String | - | - |
| expandLabelClassName | 展开列标题的自定义类名 | String | - | - |
| border | 是否带有纵向边框 | boolean | - | false |
| reserveSelection | 在数据更新之后保留之前选中的数据（需指定 rowKey） | boolean | - | false |
| fit | 列的宽度是否自撑开 | boolean | - | true |
| showHeader | 是否显示表头 | boolean | - | true |
| header | 隐藏表格头部操作 | boolean | - | false |
| highlightCurrentRow | 是否要高亮当前行 | boolean | - | false |
| rowKey | 行数据的 Key，用来优化 Table 的渲染；在使用 reserve-selection 功能与显示树形数据时，该属性是必填的。 | string | - | id |
| rowParentKey | 行数据的 Key，的父类Key用于局部刷新树形表格。 | string | - | parentId |
| emptyText | 空数据时显示的文本内容 | string | - | 暂无数据 |
| defaultExpandAll | 是否默认展开所有行，当前表格包含展开行存在或者为树形表格时有效 | boolean | - | false |
| expandRowKeys | 可以通过该属性设置 Table 目前的展开行，需要设置 rowKey 属性才能使用，该属性为展开行的 keys 数组。 | array | - | false |
| defaultSort | 默认的排序列的 prop 和顺序。它的prop属性指定默认的排序的列，order指定默认排序的顺序 | object | ascending/descending | ascending |
| showSummary | 是否在表尾显示合计行 | boolean | - | false |
| lazy | 是否懒加载子节点数据,会调用tree-load方法回调 | boolean | - | false |
| title | 表格标题 | string | - | - |
| addBtn | 表格新增按钮 | boolean | - | true |
| addBtnText | 表格新增按钮文案 | string | - | 新增 |
| addBtnIcon | 表格新增按钮图标 | string | - | - |
| editBtn | 表格修改按钮 | boolean | - | true |
| editBtnText | 表格修改按钮文案 | string | - | 修改 |
| editBtnIcon | 表格修改按钮图标 | string | - | - |
| delBtn | 表格删除按钮 | boolean | - | true |
| delBtnText | 表格删除按钮文案 | string | - | 删除 |
| delBtnIcon | 表格删除按钮图标 | string | - | - |
| viewBtn | 表格查看按钮 | boolean | - | false |
| viewBtnText | 表格查看按钮文案 | string | - | 查看 |
| viewBtnIcon | 表格查看按钮图标 | string | - | - |
| updateBtn | 表格弹窗修改按钮 | boolean | - | true |
| updateBtnText | 表格弹窗修改按钮文案 | string | - | 修改 |
| updateBtnIcon | 表格弹窗修改按钮图标 | string | - | - |
| saveBtn | 表格弹窗保存按钮 | boolean | - | true |
| saveBtnText | 表格弹窗保存按钮文案 | string | - | 保存 |
| saveBtnIcon | 表格弹窗保存按钮图标 | string | - | - |
| cancelBtn | 表格弹窗取消按钮 | boolean | - | true |
| cancelBtnText | 表格弹窗取消按钮文案 | string | - | 取消 |
| cancelBtnIcon | 表格弹窗取消按钮图标 | string | - | - |
| searchBtn | 表格搜索按钮 | boolean | - | true |
| searchBtnText | 表格搜索按钮文案 | string | - | 搜索 |
| searchBtnIcon | 表格搜索按钮图标 | string | - | - |
| emptyBtn | 表格清空按钮 | boolean | - | true |
| emptyBtnText | 表格清空按钮文案 | string | - | 清空 |
| emptyBtnIcon | 表格清空按钮图标 | string | - | - |
| printBtn | 表格打印按钮 | boolean | - | false |
| excelBtn | 表格导出按钮 | boolean | - | false |
| filterBtn | 表格自定义过滤按钮 | boolean | - | false |
| refreshBtn | 表格刷新数据按钮 | boolean | - | true |
| columnBtn | 表格列操作按钮 | boolean | - | true |
| searchShowBtn | 表格搜索显隐按钮 | boolean | - | true |
| copyBtn | 表格复制数据按钮 | boolean | - | false |
| gridBtn | 卡片模式切换按钮 | boolean | - | true |
| gridSpan | 卡片模式格栅 | number | - | 8 |
| gridBackgroundImage | 卡片模式背景图片 | string | - | - |
| gridBackground | 卡片模式背景颜色 | string/function | - | - |
| addTitle | 表格新增弹窗标题 | string | - | 新增 |
| editTitle | 表格修改弹窗标题 | boolean | - | 修改 |
| viewTitle | 表格查看弹窗标题 | boolean | - | 查看 |
| dialogDrag | 表格弹窗是否可以拖拽 | boolean | - | false |
| dialogFullscreen | 表格弹窗是否为全屏 | boolean | - | false |
| dialogCustomClass | 表格弹窗自定义class | string | - | - |
| dialogEscape | 表格弹窗是否可以通过按下ESC关闭 | boolean | - | true |
| dialogClickModal | 表格弹窗是否可以通过点击modal关闭 | boolean | - | false |
| dialogCloseBtn | 表格弹窗是否显示关闭按钮 | boolean | - | true |
| dialogModal | 表格弹窗是否需要遮罩层 | boolean | - | true |
| dialogMenuPosition | 表格弹窗框按钮的位置 | string | left/center/right | right |
| dialogTop | 表格弹窗顶部的距离 | number | - | 25 |
| dialogType | 表格弹窗方式 | string | dialog/drawer | dialog |
| dialogDirection | 表格弹窗打开方向 | string | rtl/ltr/ttb/tbb | rtl |
| dialogWidth | 表格弹窗宽度 | string | - | 60% |
| searchShow | 表格搜索首次是否展示 | boolean | - | true |
| searchIcon | 表格搜索半收缩按钮 | boolean | - | false |
| searchIndex | 表格搜索半收缩个数 | number | - | 2 |
| searchMenuPosition | 表格搜索按钮位置 | left/center/right | - | center |
| searchPlaceholder | 搜索项辅助文字 | string | — | - |
| searchSpan | 搜索项框栅列 | number | — | 8 |
| searchGutter | 搜索项框间距 | number | — | - |
| searchLabelWidth | 搜索项标题宽度 | number | — | 80 |
| searchLabelPosition | 搜索项标题位置 | string | left/right/top | left |

### Column-字典属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| props | 数据字典属性的配置对象，具体参考Props参考配置 | object | — | — |
| dicData | 数据字典值 | array | — | — |
| dicUrl | 数据字典接口url地址 | string | — | — |
| dicFlag | 打开表单时重新请求 | boolean | — | false |
| dicQuery | 数据字典接口url携带请求参数 | object | — | — |
| dicHeaders | 数据字典接口url携带头部参数 | object | — | — |
| dicFormatter | 数据字典接口url返回数据格式化方法 | function | — | (res)=>{return res} |
| dicMethod | 数据字典接口请求方式 | string | — | — |

### Column-Props

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| label | 选项标签为选项对象的某个属性值 | string | — | label |
| value | 选项的值为选项对象的某个属性值 | string | — | value |
| children | 选项的子选项为选项对象的某个属性值 | string | — | children |
| disabled | 选项的禁用为选项对象的某个属性值 | string | — | disabled |
| res | 选项返回结构的层级(例如data.data) | string | — | - |

### Column-共用属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| label | 列标题 | string | — | — |
| prop | 列标题的内容属性名称 | string | — | - |
| width | 对应列的宽度 | string | — | - |
| bind | 深结构数据绑定值 | string | — | - |
| minWidth | 对应列的最小宽度，与 width 的区别是 width 是固定的，minWidth 会把剩余宽度按比例分配给设置了 minWidth 的列 | string | — | - |
| fixed | 列是否固定在左侧或者右侧，true 表示固定在左侧 | boolean/string | true/left/right | - |
| className | 列的单元格自定义类名 | String | - | - |
| labelClassName | 列标题的自定义类名 | String | - | - |
| sortable | 对应列是否可以排序，如果设置为 'custom'，则代表用户希望远程排序，需要监听 Table 的 sort-change 事件 | string | true, false, 'custom' | - |
| formatter | 用来格式化列内容 | function | - | (row, value, row, column) |
| overHidden | 当内容过长被隐藏时显示 tooltip | boolean | - | false |
| align | 对齐方式 | string | left/center/right | left |
| headerAlign | 表头对齐方式，若不设置该项，则使用表格的对齐方式 | string | left/center/right | left |
| filters | 数据过滤的选项。 | boolean | - | false |
| search | 是否为搜索项 | boolean | — | false |
| searchValue | 搜索项初始化值 | string | — | - |
| searchPlaceholder | 搜索项辅助文字 | string | — | - |
| searchSpan | 搜索项框栅列 | number | — | 8 |
| searchOrder | 搜索项位置排序，序号越大越靠前 | number | — | - |
| searchGutter | 搜索项框间距 | number | — | - |
| searchRange | 搜索项为范围搜索 | boolean | — | false |
| searchType | 搜索项的类型 | string | — | - |
| searchLabelWidth | 搜索项标题宽度 | number | — | 80 |
| searchClearable | 搜索项清除 | boolean | — | false |
| searchMultiple | 搜索项是否多选 | boolean | — | false |
| searchTags | 搜索项将选中值按文字的形式展示 | boolean | — | false |
| searchLabelPosition | 搜索项标题位置 | string | left/right/top | left |
| display | 弹出表单是否显示 | boolean | - | true |
| disabled | 弹出表单是否禁止 | boolean | - | false |
| addDisabled | 表单新增时项是否禁止 | boolean | — | false |
| editDisabled | 表单编辑时项是否禁止 | boolean | — | false |
| viewDisabled | 表单查看时项是否禁止 | boolean | — | false |
| addDisplay | 表单新增时项是否显示 | boolean | — | true |
| editDisplay | 表单编辑时项是否显示 | boolean | — | true |
| viewDisplay | 表单查看时项是否显示 | boolean | — | true |
| resizable | 对应列是否可以通过拖动改变宽度（需要在option中border属性为真） | boolean | — | true |

### Events

| 事件名称 | 说明 | 参数 |
| --- | --- | --- |
| row-save | 新增数据后点击确定触发该事件 | row,done,loading |
| row-update | 更新数据后确定触发该事件 | row,index,done,loading |
| row-del | 行数据删除时触发该事件 | row,index |
| refresh-change | 点击刷新按钮触发该事件(由于page分页信息和search搜索信息是sync修饰符，可以直接通过this.page和this.search拿到) | - |
| search-change | 点击搜索后触发该事件(由于page分页信息和search搜索信息是sync修饰符，可以直接通过this.page和this.search拿到) | form,done |
| search-reset | 清空搜索回调方法 | - |
| dateChange | dateBtn为true时的选择日期回调方法 | date |
| tree-load | 加载子节点数据的函数，lazy 为 true 时生效，函数第二个参数包含了节点的层级信息 | row, treeNode, resolve) |
| select | 当用户手动勾选数据行的 Checkbox 时触发的事件 | selection, row |
| select-all | 当用户手动勾选全选 Checkbox 时触发的事件 | selection |
| selection-change | 当选择项发生变化时会触发该事件 | selection |
| cell-mouse-enter | 当单元格 hover 进入时会触发该事件 | row, column, cell, event |
| cell-mouse-leave | 当单元格 hover 退出时会触发该事件 | row, column, cell, event |
| cell-click | 当某个单元格被点击时会触发该事件 | row, column, cell, event |
| cell-dblclick | 当某个单元格被双击击时会触发该事件 | row, column, cell, event |
| row-click | 当某一行被点击时会触发该事件 | row, column, event |
| row-contextmenu | 当某一行被鼠标右键点击时会触发该事件 | row, column, event |
| row-dblclick | 当某一行被双击时会触发该事件 | row, column, event |
| header-click | 当某一列的表头被点击时会触发该事件 | column, event |
| header-contextmenu | 当某一列的表头被鼠标右键点击时触发该事件 | column, event |
| sort-change | 当表格的排序条件发生变化的时候会触发该事件 | { column, prop, order } |
| filter-change | 当表格的筛选条件发生变化的时候会触发该事件，参数的值是一个对象，对象的 key 是 column 的 columnKey，对应的 value 为用户选择的筛选条件的数组。 | filters |
| current-row-change | 当表格的当前行发生变化的时候会触发该事件，如果要高亮当前行，请打开表格的 highlightCurrentRow 属性 | currentRow, oldCurrentRow |
| grid-status-change2.12.7 | table模式和 grid模式切换回调 | status |
| header-dragend | 当拖动表头改变了列的宽度的时候会触发该事件 | newWidth, oldWidth, column, event |
| expand-change | 当用户对某一行展开或者关闭的时候会触发该事件（展开行时，回调的第二个参数为 expandedRows；树形表格时第二参数为 expanded） | row, (expandedRows |

### Methods

| 事件名称 | 说明 | 参数 |
| --- | --- | --- |
| rowAdd | 打开表单新增窗口 | - |
| rowEdit | 打开表单编辑窗口 | row,index |
| rowView | 打开表单查看窗口 | row,index |
| updateDic | 更新指定字典 | prop,dic |
| dicInit | 重新加载全部字典 | - |
| getPropRef | 获取prop的ref对象 | prop |
| validate | 对整个表单进行校验的方法，参数为一个回调函数。该回调函数会在校验结束后被调用，并传入两个参数：是否校验成功和未通过校验的字段。若不传入回调函数，则会返回一个 promise | (valid,done,msg) |
| validateField | 对部分表单字段进行校验的方法 | Function(props: array |
| resetFields | 对整个表单进行重置，将所有字段值重置为初始值并移除校验结果 | - |
| clearValidate | 移除表单项的校验结果。传入待移除的表单项的 prop 属性或者 prop 组成的数组，如不传则移除整个表单的校验结果 | Function(props: array |
| clearSelection | 用于多选表格，清空用户的选择 | - |
| toggleSelection | 用于多选表格，传递数组进去，会勾选数组中的对象，如果已经勾选则会取消勾选 | array |
| toggleRowSelection | 用于多选表格，切换某一行的选中状态，如果使用了第二个参数，则是设置这一行选中与否（selected 为 true 则选中） | row, selected |
| toggleAllSelection | 用于多选表格，切换所有行的选中状态 | - |
| toggleRowExpansion | 用于可展开表格与树形表格，切换某一行的展开状态，如果使用了第二个参数，则是设置这一行展开与否（expanded 为 true 则展开） | row, expanded |
| setCurrentRow | 用于单选表格，设定某一行为选中行，如果调用时不加参数，则会取消目前高亮行的选中状态。 | row |
| clearSort | 用于清空排序条件，数据会恢复成未排序的状态 | - |
| clearFilter | 不传入参数时用于清空所有过滤条件，数据会恢复成未过滤的状态，也可传入由columnKey组成的数组以清除指定列的过滤条件 | columnKey |
| doLayout | 对 Table 进行重新布局。当 Table 或其祖先元素由隐藏切换为显示时，可能需要调用此方法 | - |
| refreshTable | 进行重新初始化渲染 | - |
| sort | 手动对 Table 进行排序。参数prop属性指定排序列，order指定排序顺序。 | prop: string, order: string |

### Slot

| 名称 | 说明 |
| --- | --- |
| 'prop' | 列 |
| 'prop'Header | 列头部 |
| 'prop'Search | 列搜索 |
| 'prop'Form | 弹窗表单 |
| 'prop'Label | 弹窗表单的标题 |
| 'prop'Error | 弹窗表单错误提示 |
| search | 表格搜索 |
| searchMenu | 表格搜索菜单 |
| header | 表格头部 |
| body | 表格中部 |
| page | 表格分页 |
| menuLeft | 表格菜单左部分 |
| menuRight | 表格菜单右部分 |
| menu | 表格菜单 |
| menuBefore | 表格菜单前 |
| menuBtn | 表格合并菜单 |
| menuBtnBefore | 表格合并菜单前 |
| menuForm | 表格弹窗菜单 |
| menuFormBefore | 表格弹窗菜单前 |

[Object对象形式](https://v2.avuejs.com/crud/crud-object/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号