动态行列合并
======

```vue
<avue-crud
  :data="data"
  :option="option"
  :span-method="spanMethod"
></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          { name: '王小虎', sex: '男', grade: '级别1', amount1: '234', amount2: '3.2', amount3: 10 },
          { name: '王小虎', sex: '男', grade: '级别2', amount1: '165', amount2: '4.43', amount3: 12 },
          { name: '王三虎', sex: '女', grade: '级别2', amount1: '539', amount2: '4.1', amount3: 15 },
          { name: '王三虎', sex: '女', grade: '级别1', amount1: '539', amount2: '4.1', amount3: 15 },
          { name: '王小虎', sex: '男', grade: '级别3', amount1: '324', amount2: '1.9', amount3: 9 },
          { name: '王小虎', sex: '女', grade: '级别1', amount1: '621', amount2: '2.2', amount3: 17 },
          { name: '王小虎', sex: '女', grade: '级别1', amount1: '539', amount2: '4.1', amount3: 15 },
          { name: '王大虎', sex: '男', grade: '级别2', amount1: '539', amount2: '4.1', amount3: 15 },
          { name: '王小虎', sex: '男', grade: '级别1', amount1: '539', amount2: '4.1', amount3: 15 },
          { name: '王大虎', sex: '女', grade: '级别2', amount1: '539', amount2: '4.1', amount3: 15 }
        ],
        option: {
          border: true,
          column: [
            { label: '姓名', prop: 'name' },
            { label: '年龄', prop: 'sex' },
            { label: '数值 1', prop: 'amount1' },
            { label: '数值 2', prop: 'amount2' },
            { label: '数值 3', prop: 'amount3' },
            { label: '权限', prop: 'grade' }
          ]
        },
        spanArr: [
          { prop: 'name', span: [] },
          { prop: 'sex', span: [] },
          { prop: 'grade', span: [] }
        ]
      }
    },
    created() {
      this.rowSort()
      this.rowCalc()
    },
    methods: {
      rowCalc() {
        this.spanArr.forEach((ele, index) => {
          let parent
          if (index !== 0) parent = this.spanArr[ele.parent || index - 1].span
          ele.span = this.rowSpan(ele.prop, parent)
        })
      },
      rowSort() {
        this.spanArr.forEach((ele, index) => {
          let key = ele.prop
          this.data = this.data.sort((a, b) => {
            let flag = true
            for (let i = 0; i < index; i++) {
              let prop = this.spanArr[i].prop
              flag = flag && a[prop] == b[prop]
            }
            if (flag) {
              if (a[key] < b[key]) return 1
              else if (a[key] > b[key]) return -1
              return 0
            }
            return 0
          })
        })
      },
      rowSpan(key, parent) {
        let list = []
        let position = 0
        this.data.forEach((item, index) => {
          if (index === 0) {
            list.push(1)
            position = 0
          } else {
            if (this.data[index][key] === this.data[index - 1][key]) {
              if (parent && parent[index] !== 0) {
                list.push(1)
                position = index
              } else {
                list[position] += 1
                list.push(0)
              }
            } else {
              list.push(1)
              position = index
            }
          }
        })
        return list
      },
      spanMethod({ row, column, rowIndex, columnIndex }) {
        for (let i = 0; i < this.spanArr.length; i++) {
          const ele = this.spanArr[i]
          if (column.property == ele.prop) {
            const _row = ele.span[rowIndex]
            const _col = _row > 0 ? 1 : 0
            return {
              rowspan: _row,
              colspan: _col
            }
          }
        }
      }
    }
  }
</script>
```