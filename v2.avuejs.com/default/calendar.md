Calendar日历
==========

* 2020
* 2021
* 2022
* 2023
* 2024
* 2025
* 2026
* 2027

无数据

* 1月
* 2月
* 3月
* 4月
* 5月
* 6月
* 7月
* 8月
* 9月
* 10月
* 11月
* 12月

无数据

* 元旦节
* 除夕
* 春节
* 清明节
* 劳动节
* 端午节
* 中秋节
* 国庆节

无数据

返回今天

2025 年 3 月

上个月 今天 下个月

| 一   | 二   | 三   | 四   | 五   | 六   | 日   |
| --- | --- | --- | --- | --- | --- | --- |
| **24** 正月廿七 | **25** 正月廿八 | **26** 正月廿九 | **27** 正月三十 | **28** 二月初一 | **01** 二月初二 | **02** 二月初三 |
| **03** 二月初四 | **04** 二月初五 | **05** 二月初六 | **06** 二月初七 | **07** 二月初八 | **08** 二月初九 | **09** 二月初十 |
| **10** 二月十一 | **11** 二月十二 | **12** 二月十三 | **13** 二月十四 | **14** 二月十五 | **15** 二月十六 | **16** 二月十七 |
| **17** 二月十八 | **18** 二月十九 | **19** 二月二十 | **20** 二月廿一 | **21** 二月廿二 | **22** 二月廿三 | **23** 二月廿四 |
| **24** 二月廿五 | **25** 二月廿六 | **26** 二月廿七 | **27** 二月廿八 | **28** 二月廿九 | **29** 三月初一 | **30** 三月初二 |
| **31** 三月初三 | **01** 三月初四 | **02** 三月初五 | **03** 三月初六 | **04** 三月初七 | 休 **05** 清明节 | **06** 三月初九 |

<div class="avue-calendar">
  <div class="avue-calendar__header">
    <el-select v-model="year" @change="handleYear">
      <el-option v-for="item in year_list" :key="item.value" :label="item.label" :value="item.value"></el-option>
    </el-select>
    <el-select v-model="month" @change="handleMonth">
      <el-option v-for="item in month_list" :key="item.value" :label="item.label" :value="item.value"></el-option>
    </el-select>
    <el-select v-model="select" placeholder="假期安排" @change="handleSelect">
      <el-option v-for="item in list" :key="item.value" :label="item.label" :value="item.value"></el-option>
    </el-select>
    <el-button type="primary" @click="goNowDay">返回今天</el-button>
  </div>
  <div class="avue-calendar__body">
    <el-calendar ref="calendar" v-model="date">
      <template slot="dateCell" slot-scope="{date, data}">
        <div class="item" :class="{'is-xiu':corXiu(date),'is-select':data.isSelected}">
          <small class="tip" v-if="corXiu(date)">休</small>
          <b class="title">{{ data.day.split('-').slice(1)[1] }}</b>
          <small class="subtitle">{{corDate(date)}}</small>
        </div>
      </template>
    </el-calendar>
  </div>
</div>

<script>
const date = new Date()
const calendar = {
  lunarInfo: [0x04bd8, 0x04ae0, 0x0a570, /*...省略数据以节省篇幅...*/ 0x0d520], // 1900-2100润大小信息表
  solarMonth: [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
  Gan: ["甲","乙","丙","丁","戊","己","庚","辛","壬","癸"],
  Zhi: ["子","丑","寅","卯","辰","巳","午","未","申","酉","戌","亥"],
  Animals: ["鼠", "牛", "虎", "兔", "龙", "蛇", "马", "羊", "猴", "鸡", "狗", "猪"],
  solarTerm: ["小寒", "大寒", "立春", "雨水", "惊蛰", "春分", "清明", "谷雨", "立夏", "小满", "芒种", "夏至", "小暑", "大暑", "立秋", "处暑", "白露", "秋分", "寒露", "霜降", "立冬", "小雪", "大雪", "冬至"],
  sTermInfo: ['9778397bd097c36b0b6fc9274c91aa', /*...省略数据以节省篇幅...*/],
  nStr1: ["日", "一", "二", "三", "四", "五", "六", "七", "八", "九", "十"],
  nStr2: ["初", "十", "廿", "卅"],
  nStr3: ["正", "二", "三", "四", "五", "六", "七", "八", "九", "十", "冬", "腊"],
  lYearDays(y) {
    let sum = 348;
    for (let i = 0x8000; i > 0x8; i >>= 1) { sum += (this.lunarInfo[y - 1900] & i) ? 1 : 0; }
    return (sum + this.leapDays(y));
  },
  leapMonth(y) {
    return (this.lunarInfo[y - 1900] & 0xf);
  },
  leapDays(y) {
    if(this.leapMonth(y)) return ((this.lunarInfo[y - 1900] & 0x10000) ? 30 : 29);
    return 0;
  },
  monthDays(y, m) {
    if(m > 12 || m < 1) return -1;
    return ((this.lunarInfo[y - 1900] & (0x10000 >> m)) ? 30 : 29);
  },
  solarDays(y, m) {
    if(m > 12 || m < 1) return -1;
    if(m === 2) return ((y%4 === 0 && y%100 !== 0) || (y%400 === 0)) ? 29 : 28;
    return this.solarMonth[m-1];
  },
  toGanZhiYear(lYear) {
    let ganKey = (lYear - 3) % 10 || 10;
    let zhiKey = (lYear - 3) % 12 || 12;
    return this.Gan[ganKey - 1] + this.Zhi[zhiKey - 1];
  },
  toAstro(cMonth, cDay) {
    const s = "魔羯水瓶双鱼白羊金牛双子巨蟹狮子处女天秤天蝎射手魔羯";
    const arr = [20,19,21,21,21,22,23,23,23,23,22,22];
    return s.substr(cMonth*2-(cDay<arr[cMonth-1]?2:0),2)+'座';
  },
  toGanZhi(offset) {
    return this.Gan[offset % 10] + this.Zhi[offset % 12];
  },
  getTerm(y, n) {
    if(y < 1900 || y>2100 || n<1 || n>24) return -1;
    const _table = this.sTermInfo[y - 1900];
    const _info = [
      parseInt('0x'+_table.substr(0,5)).toString(),
      parseInt('0x'+_table.substr(5,5)).toString(),
      parseInt('0x'+_table.substr(10,5)).toString(),
      parseInt('0x'+_table.substr(15,5)).toString(),
      parseInt('0x'+_table.substr(20,5)).toString(),
      parseInt('0x'+_table.substr(25,5)).toString()
    ];
    const _calday = [
      _info[0].substr(0,1), _info[0].substr(1,2), _info[0].substr(3,1), _info[0].substr(4,2),
      _info[1].substr(0,1), _info[1].substr(1,2), _info[1].substr(3,1), _info[1].substr(4,2),
      _info[2].substr(0,1), _info[2].substr(1,2), _info[2].substr(3,1), _info[2].substr(4,2),
      _info[3].substr(0,1), _info[3].substr(1,2), _info[3].substr(3,1), _info[3].substr(4,2),
      _info[4].substr(0,1), _info[4].substr(1,2), _info[4].substr(3,1), _info[4].substr(4,2),
      _info[5].substr(0,1), _info[5].substr(1,2), _info[5].substr(3,1), _info[5].substr(4,2),
    ];
    return parseInt(_calday[n - 1]);
  },
  toChinaMonth(m) {
    if(m > 12 || m < 1) return -1;
    return this.nStr3[m-1] + "月";
  },
  toChinaDay(d) {
    switch(d) {
      case 10: return '初十';
      case 20: return '二十';
      case 30: return '三十';
      default: return this.nStr2[Math.floor(d/10)] + this.nStr1[d%10];
    }
  },
  getAnimal(y) {
    return this.Animals[(y-4) % 12];
  },
  solar2lunar(y,m,d) {
    if(y<1900||y>2100) return -1;
    if(y===1900 && m===1 && d<31) return -1;
    if(!y) {
      var objDate=new Date();
    } else {
      var objDate=new Date(y,m-1,d);
    }
    y=objDate.getFullYear(); m=objDate.getMonth()+1; d=objDate.getDate();
    let offset=(Date.UTC(y,m-1,d)-Date.UTC(1900,0,31))/86400000;
    let i,temp=0;
    for(i=1900; i<2101 && offset>0; i++) {
      temp=this.lYearDays(i);
      offset-=temp;
    }
    if(offset<0) { offset+=temp; i--; }
    let leap=this.leapMonth(i), isLeap=false;
    for(let j=1; j<13 && offset>0; j++) {
      if(leap>0 && j==leap+1 && !isLeap) { j--; isLeap=true; temp=this.leapDays(i); }
      else temp=this.monthDays(i,j);
      if(isLeap && j==leap+1) isLeap=false;
      offset-=temp;
    }
    if(offset===0 && leap>0 && i===leap+1) {
      if(isLeap) isLeap=false;
      else { isLeap=true; i--; }
    }
    if(offset<0) { offset+=temp; i--; }
    let month=i;
    let day=offset+1;
    let gzY=this.toGanZhiYear(i);
    let firstNode=this.getTerm(y,m*2-1);
    let secondNode=this.getTerm(y,m*2);
    let gzM=this.toGanZhi((y-1900)*12 + m + 11);
    if(d>=firstNode) gzM=this.toGanZhi((y-1900)*12 + m + 12);
    let isTerm=false, Term=null;
    if(firstNode===d) { isTerm=true; Term=this.solarTerm[m*2-2]; }
    if(secondNode===d) { isTerm=true; Term=this.solarTerm[m*2-1]; }
    let dayCyclical=Date.UTC(y,m-1,1)/86400000 + 25567 + 10;
    let gzD=this.toGanZhi(dayCyclical+d-1);
    let astro=this.toAstro(m,d);
    let isTodayObj=new Date(), isToday=false;
    if(isTodayObj.getFullYear()===y && isTodayObj.getMonth()+1===m && isTodayObj.getDate()===d) isToday=true;
    let nWeek=objDate.getDay(), cWeek=this.nStr1[nWeek];
    if(nWeek===0) nWeek=7;
    return {
      'lYear': i, 'lMonth': month, 'lDay': day, 'Animal': this.getAnimal(i),
      'IMonthCn': (isLeap ? "闰" : '') + this.toChinaMonth(month), 'IDayCn': this.toChinaDay(day),
      'cYear': y, 'cMonth': m, 'cDay': d, 'gzYear': gzY, 'gzMonth': gzM, 'gzDay': gzD,
      'isToday': isToday, 'isLeap': isLeap, 'nWeek': nWeek, 'ncWeek': "星期" + cWeek,
      'isTerm': isTerm, 'Term': Term, 'astro': astro
    };
  },
  lunar2solar(y,m,d,isLeapMonth) {
    isLeapMonth=!!isLeapMonth;
    let leapMonth=this.leapMonth(y);
    if(isLeapMonth && leapMonth!==m) return -1;
    if((y===2100 && m===12 && d>1) || (y===1900 && m===1 && d<31)) return -1;
    let day=this.monthDays(y,m), _day=day;
    if(isLeapMonth) _day=this.leapDays(y,m);
    if(y<1900 || y>2100 || d>_day) return -1;
    let offset=0, isAdd=false, leap=0;
    for(let i=1900; i<y; i++) offset+=this.lYearDays(i);
    for(let i=1; i<m; i++) {
      leap=this.leapMonth(y);
      if(!isAdd && leap<=i && leap>0) {
        offset+=this.leapDays(y);
        isAdd=true;
      }
      offset+=this.monthDays(y,i);
    }
    if(isLeapMonth) offset+=day;
    let stmap=Date.UTC(1900,1,30,0,0,0);
    let calObj=new Date((offset+d-31)*86400000 + stmap);
    let cY=calObj.getUTCFullYear(), cM=calObj.getUTCMonth()+1, cD=calObj.getUTCDate();
    return this.solar2lunar(cY,cM,cD);
  }
};

const getNumber = val => {
  const dic = {零:0, 一:1, 二:2, 三:3, 四:4, 五:5, 六:6, 七:7, 八:8, 九:9, 十:10};
  return dic[val] + '';
}

const lunar2solar = val => {
  const monthList = [{label: '正', value: 1}, {label: '冬', value: 11}, {label: '腊', value: 12}];
  const result = val.split('月');
  let month, day;
  let obj = monthList.find(ele => ele.label == result[0]);
  if(obj) month = obj.value;
  else month = getNumber(result[0]);
  const dayFirst = result[1].charAt(0);
  day = result[1].substr(1);
  if(dayFirst == '初') day = getNumber(day);
  else if(dayFirst == '十') day = 10 + getNumber(day);
  else if(dayFirst == '二') day = 20;
  else if(dayFirst == '廿') day = 20 + getNumber(day);
  else if(dayFirst == '三') day = 30;
  day = Number(day);
  month = Number(month);
  return { month, day };
}

export default {
  data() {
    return {
      year: date.getFullYear(),
      month: date.getMonth(),
      year_list: [
        {label: '2020', value: 2020}, {label: '2021', value: 2021}, {label: '2022', value: 2022},
        {label: '2023', value: 2023}, {label: '2024', value: 2024}, {label: '2025', value: 2025},
        {label: '2026', value: 2026}, {label: '2027', value: 2027}
      ],
      month_list: new Array(12).fill({}).map((ele, index) => ({ label: (index + 1) + '月', value: index })),
      select: '',
      date: date,
      list: [
        {label: '元旦节', value: '1-1', list: ['12-31','1-1','1-2']},
        {label: '除夕', value: '腊月三十', old: true, filter: ['2020','2022','2025','2026','2028','2029'], list: ['腊月三十']},
        {label: '春节', value: '正月初一', list: ['正月初一','正月初二','正月初三','正月初四','正月初五','正月初六']},
        {label: '清明节', value: '4-5', list: ['4-5']},
        {label: '劳动节', value: '5-1', list: ['4-29','4-30','5-1','5-2','5-3']},
        {label: '端午节', value: '五月初五', list: ['五月初五','五月初六','五月初七']},
        {label: '中秋节', value: '八月十五', list: ['八月十五','八月十六','八月十七']},
        {label: '国庆节', value: '10-1', list: ['10-1','10-2','10-3','10-4','10-5','10-6']}
      ]
    }
  },
  watch: {
    date(val) {
      this.year = val.getFullYear();
      this.month = val.getMonth();
    }
  },
  methods: {
    goNowDay() {
      this.date = date;
    },
    handleYear(val) {
      this.date = new Date(val, this.month, this.date.getDate());
      this.select = '';
    },
    handleMonth(val) {
      this.date = new Date(this.year, val, this.date.getDate());
      this.select = '';
    },
    handleSelect(val) {
      const item = this.list.find(ele => ele.value == val);
      if(item) {
        if(val.indexOf('-') == -1) {
          let {month, day} = lunar2solar(val);
          if(item.filter) {
            let obj = item.filter.find(ele => ele == this.year);
            if(obj) day = day - 1;
          }
          let format = calendar.lunar2solar(item.old ? this.year - 1 : this.year, month, day);
          this.date = new Date(this.year, format.cMonth - 1, format.cDay);
        } else {
          const array = val.split('-');
          this.date = new Date(this.year, array[0] - 1, array[1]);
        }
      }
    },
    corXiu(date) {
      let yy = date.getFullYear(), mm = date.getMonth() + 1, dd = date.getDate();
      const format = calendar.solar2lunar(yy, mm, dd);
      let result = false;
      this.list.forEach(ele => {
        ele.list.forEach(item => {
          if(item.indexOf('-') == -1) {
            let {month, day} = lunar2solar(item);
            if(month == format.lMonth && day == format.lDay) result = true;
          } else {
            const array = item.split('-');
            if(mm == array[0] && dd == array[1]) result = true;
          }
        });
      });
      return result;
    },
    corDate(date) {
      let yy = date.getFullYear(), mm = date.getMonth() + 1, dd = date.getDate();
      const format = calendar.solar2lunar(yy, mm, dd);
      const obj = this.list.find(ele => {
        if(ele.value == format.IMonthCn + format.IDayCn) return true;
        else if(ele.value == format.cMonth + '-' + format.cDay) return true;
        return false;
      });
      if(obj) return obj.label;
      else return `${format.IMonthCn}${format.IDayCn}`;
    }
  }
}
</script>

<style lang="scss">
.avue-calendar {
  width: 850px;
  &__header {
    margin-bottom: 10px;
    .el-select {
      margin-right: 10px;
    }
  }
  &__body {
    padding: 20px 5px;
    border: 2px solid #409eff;
    border-radius: 5px;
  }
  .el-calendar-table {
    .el-calendar-day:hover {
      background-color: transparent;
    }
    td.is-selected {
      background-color: transparent;
    }
    tr td {
      border: none;
    }
    .el-calendar-day {
      padding: 2px;
    }
    .is-today {
      .item {
        border: 2px solid #409eff;
        .title {
          color: #409eff;
        }
        .subtitle {
          color: #409eff;
        }
      }
    }
    .item {
      box-sizing: border-box;
      border: 2px solid #fff;
      position: relative;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      line-height: 25px;
      border-radius: 5px;
      &:hover {
        border: 2px solid #bdbfc8;
      }
    }
    .tip {
      position: absolute;
      left: 5px;
      top: 0px;
    }
    .title {
      font-size: 24px;
    }
    .subtitle {
      margin-top: 2px;
      color: #999;
    }
    .is-xiu {
      color: #f73131;
      background-color: #fde3e4;
      &:hover {
        border: 2px solid #f38686;
      }
      &.is-select {
        color: #f73131;
        border: 2px solid #f38686;
      }
      .subtitle {
        color: #f73131;
        font-weight: bold;
      }
    }
    .is-select {
      color: #333;
      border: 2px solid #bdbfc8;
    }
  }
}
</style>