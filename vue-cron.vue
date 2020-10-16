<style lang="less" scoped>
.content {
  .language {
    position: absolute;
    right: 25px;
    z-index: 1;
  }

  .el-tabs {
    box-shadow: none;
  }

  .el-icon-date {
    margin-right: 0.25em;
  }

  .tab-body {
    .el-row {
      margin: 10px 0;

      .long {
        .el-select {
          width: 350px;
        }
      }

      .el-input-number {
        width: 110px;
      }

      .short-select {
        width: 8em;
      }
    }
  }

  .bottom {
    width: 100%;
    text-align: right;
    margin-top: 5px;
    position: relative;

    .value {
      font-size: 18px;
      vertical-align: middle;
    }
  }
}
</style>
<template>
  <div class="content">
    <el-tabs type="border-card">
      <el-tab-pane>
        <span slot="label"> <i class="el-icon-date"></i>秒 </span>
        <div class="tab-body">
          <el-row>
            <el-radio v-model="second.cronEvery" label="1"
              >每秒 允许的通配符[, - * /]</el-radio
            >
          </el-row>
          <el-row>
            <el-radio v-model="second.cronEvery" label="2">
              周期从&emsp;
              <el-input-number
                v-model="second.rangeStart"
                :min="1"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;到&emsp;
              <el-input-number
                v-model="second.rangeEnd"
                :min="1"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;秒钟
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="second.cronEvery" label="3">
              从&emsp;
              <el-input-number
                v-model="second.intervalStart"
                :min="0"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;秒钟开始，每&emsp;
              <el-input-number
                v-model="second.interval"
                :min="1"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;秒钟执行一次
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="second.cronEvery" label="4">
              指定&emsp;
              <el-select v-model="second.specifics" multiple placeholder>
                <el-option
                  v-for="(item, index) in 60"
                  :key="item"
                  :value="index"
                  >{{ index }}</el-option
                >
              </el-select>
            </el-radio>
          </el-row>
        </div>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label"> <i class="el-icon-date"></i>分 </span>
        <div class="tab-body">
          <el-row>
            <el-radio v-model="minute.cronEvery" label="1"
              >每分钟 允许的通配符[, - * /]</el-radio
            >
          </el-row>
          <el-row>
            <el-radio v-model="minute.cronEvery" label="2">
              周期从&emsp;
              <el-input-number
                v-model="minute.rangeStart"
                :min="1"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;到&emsp;
              <el-input-number
                v-model="minute.rangeEnd"
                :min="1"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;分钟
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="minute.cronEvery" label="3">
              从&emsp;
              <el-input-number
                v-model="minute.intervalStart"
                :min="0"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;分钟开始，每&emsp;
              <el-input-number
                v-model="minute.interval"
                :min="1"
                :max="59"
                placeholder
              ></el-input-number
              >&emsp;分钟执行一次
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="minute.cronEvery" label="4">
              指定&emsp;
              <el-select v-model="minute.specifics" multiple placeholder>
                <el-option
                  v-for="(item, index) in 60"
                  :key="item"
                  :value="index"
                  >{{ index }}</el-option
                >
              </el-select>
            </el-radio>
          </el-row>
        </div>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label"> <i class="el-icon-date"></i>时 </span>
        <div class="tab-body">
          <el-row>
            <el-radio v-model="hour.cronEvery" label="1"
              >每小时 允许的通配符[, - * /]</el-radio
            >
          </el-row>
          <el-row>
            <el-radio v-model="hour.cronEvery" label="2">
              周期从&emsp;
              <el-input-number
                v-model="hour.rangeStart"
                :min="0"
                :max="23"
                placeholder
              ></el-input-number
              >&emsp;到&emsp;
              <el-input-number
                v-model="hour.rangeEnd"
                :min="0"
                :max="23"
                placeholder
              ></el-input-number
              >&emsp;小时
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="hour.cronEvery" label="3">
              从&emsp;
              <el-input-number
                v-model="hour.intervalStart"
                :min="0"
                :max="23"
                placeholder
              ></el-input-number
              >&emsp;小时开始，每&emsp;
              <el-input-number
                v-model="hour.interval"
                :min="0"
                :max="23"
                placeholder
              ></el-input-number
              >&emsp;小时执行一次
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="hour.cronEvery" label="4">
              指定&emsp;
              <el-select v-model="hour.specifics" multiple placeholder>
                <el-option
                  v-for="(item, index) in 24"
                  :key="item"
                  :value="index"
                  >{{ index }}</el-option
                >
              </el-select>
            </el-radio>
          </el-row>
        </div>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label">
          <i class="el-icon-date"></i>
          日
        </span>
        <div class="tab-body">
          <el-row>
            <el-radio v-model="day.cronEvery" label="1"
              >每日 允许的通配符[, - * / L W]</el-radio
            >
          </el-row>
          <el-row>
            <el-radio v-model="day.cronEvery" label="2">不指定</el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="day.cronEvery" label="3">
              周期从&emsp;
              <el-input-number
                v-model="day.rangeStart"
                :min="1"
                :max="31"
                placeholder
              ></el-input-number
              >&emsp;到&emsp;
              <el-input-number
                v-model="day.rangeEnd"
                :min="1"
                :max="31"
                placeholder
              ></el-input-number>
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="day.cronEvery" label="4">
              从&emsp;
              <el-input-number
                v-model="day.intervalStart"
                :min="1"
                :max="31"
                placeholder
              ></el-input-number
              >&emsp;日开始，每&emsp;
              <el-input-number
                v-model="day.interval"
                :min="1"
                :max="31"
                placeholder
              ></el-input-number
              >&emsp;天执行一次
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="day.cronEvery" label="5">
              每月&emsp;
              <el-input-number
                v-model="day.specificW"
                :min="1"
                :max="31"
                placeholder
              ></el-input-number
              >&emsp;号最近的那个工作日
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="day.cronEvery" label="6">本月最后一天</el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="day.cronEvery" label="7">
              指定&emsp;
              <el-select v-model="day.specifics" multiple placeholder>
                <el-option v-for="item in 31" :key="item" :value="item">{{
                  item
                }}</el-option>
              </el-select>
            </el-radio>
          </el-row>
        </div>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label">
          <i class="el-icon-date"></i>
          月
        </span>
        <div class="tab-body">
          <el-row>
            <el-radio v-model="month.cronEvery" label="1"
              >月 允许的通配符[, - * /]</el-radio
            >
          </el-row>
          <el-row>
            <el-radio v-model="month.cronEvery" label="2">不指定</el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="month.cronEvery" label="3">
              周期从&emsp;
              <el-input-number
                v-model="month.rangeStart"
                :min="1"
                :max="12"
              ></el-input-number
              >&emsp;到&emsp;
              <el-input-number
                v-model="month.rangeEnd"
                :min="1"
                :max="12"
              ></el-input-number>
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="month.cronEvery" label="4">
              从&emsp;
              <el-input-number
                v-model="month.intervalStart"
                :min="1"
                :max="31"
                placeholder
              ></el-input-number
              >&emsp;日开始，每&emsp;
              <el-input-number
                v-model="month.interval"
                :min="1"
                :max="12"
                placeholder
              ></el-input-number
              >&emsp;月执行一次
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="month.cronEvery" label="5">
              指定&emsp;
              <el-select v-model="month.specifics" multiple placeholder>
                <el-option v-for="item in 31" :key="item" :value="item">{{
                  item
                }}</el-option>
              </el-select>
            </el-radio>
          </el-row>
        </div>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label"> <i class="el-icon-date"></i>周 </span>
        <div class="tab-body">
          <el-row>
            <el-radio v-model="week.cronEvery" label="1"
              >周 允许的通配符[, - * / L #]</el-radio
            >
          </el-row>
          <el-row>
            <el-radio v-model="week.cronEvery" label="2">不指定</el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="week.cronEvery" label="3">
              周期从星期&emsp;
              <el-select
                v-model="week.rangeStart"
                placeholder
                class="short-select"
              >
                <el-option
                  v-for="(item, index) in weekArr"
                  :label="item"
                  :value="index"
                  :key="item"
                  >{{ item }}</el-option
                > </el-select
              >&emsp;到&emsp;
              <el-select
                v-model="week.rangeEnd"
                placeholder
                class="short-select"
              >
                <el-option
                  v-for="(item, index) in weekArr"
                  :key="item"
                  :label="item"
                  :value="index"
                  >{{ item }}</el-option
                >
              </el-select>
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="week.cronEvery" label="4">
              第&emsp;
              <el-input-number
                v-model="week.specific"
                :min="1"
                :max="5"
                placeholder
              ></el-input-number
              >&emsp;的星期&emsp;
              <el-select
                v-model="week.specificDay"
                placeholder
                class="short-select"
              >
                <el-option
                  v-for="(item, index) in weekArr"
                  :key="item"
                  :label="item"
                  :value="index"
                  >{{ item }}</el-option
                >
              </el-select>
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="week.cronEvery" label="5">
              本月最后一个星期&emsp;
              <el-select
                v-model="week.lastWeek"
                placeholder
                class="short-select"
              >
                <el-option
                  v-for="(item, index) in weekArr"
                  :key="item"
                  :label="item"
                  :value="index"
                  >{{ item }}</el-option
                >
              </el-select>
            </el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="week.cronEvery" label="6">
              指定&emsp;
              <el-select v-model="week.specifics" multiple placeholder>
                <el-option
                  v-for="(item, index) in weekArr"
                  :key="item"
                  :label="item"
                  :value="index"
                  >{{ item }}</el-option
                >
              </el-select>
            </el-radio>
          </el-row>
        </div>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label">
          <i class="el-icon-date"></i>
          年
        </span>
        <div class="tab-body">
          <el-row>
            <el-radio v-model="year.cronEvery" label="1">每年</el-radio>
          </el-row>
          <el-row>
            <el-radio v-model="year.cronEvery" label="2">不指定</el-radio>
          </el-row>

          <el-row>
            <el-radio v-model="year.cronEvery" label="3">
              周期 从&emsp;
              <el-input-number
                v-model="year.rangeStart"
                :min="2020"
                :max="2099"
                size="small"
              ></el-input-number
              >&emsp;到&emsp;
              <el-input-number
                v-model="year.rangeEnd"
                :min="2020"
                :max="2099"
                size="small"
              ></el-input-number
              >&emsp;年
            </el-radio>
          </el-row>
        </div>
      </el-tab-pane>
    </el-tabs>
    <div class="bottom">
      <span class="value">{{ cron }}</span
      >&emsp;
      <el-button @click="close">关闭</el-button>
      <el-button type="primary" @click="change">保存</el-button>
    </div>
  </div>
</template>
<script>
const weekArr = [
  '星期天',
  '星期一',
  '星期二',
  '星期三',
  '星期四',
  '星期五',
  '星期六',
]

export default {
  name: 'VueCron',
  // props: ['data', 'value'],
  props: {
    data: {
      type: String,
      default: '* * * * * *',
    },
    value: {
      type: String,
      default: '* * * * * *',
    },
  },
  data() {
    return {
      second: {
        cronEvery: '',
        intervalStart: 1,
        interval: 5,
        rangeStart: 1,
        rangeEnd: 2,
        specifics: [],
      },
      minute: {
        cronEvery: '',
        intervalStart: 1,
        interval: 5,
        rangeStart: 1,
        rangeEnd: 2,
        specifics: [],
      },
      hour: {
        cronEvery: '',
        intervalStart: 1,
        interval: 5,
        rangeStart: 1,
        rangeEnd: 2,
        specifics: [],
      },
      day: {
        cronEvery: '',
        intervalStart: 1,
        interval: 5,
        rangeStart: 1,
        rangeEnd: 2,
        specifics: [],
        specificW: 1,
      },
      month: {
        cronEvery: '',
        intervalStart: 1,
        interval: 5,
        rangeStart: 1,
        rangeEnd: 2,
        specifics: [],
      },
      week: {
        cronEvery: '',
        rangeStart: 1,
        rangeEnd: 2,
        specific: 1,
        specificDay: 1,
        lastWeek: 1,
        specifics: [],
      },
      year: {
        cronEvery: '',
        rangeStart: 2020,
        rangeEnd: 2099,
      },
      output: {
        second: '',
        minute: '',
        hour: '',
        day: '',
        month: '',
        Week: '',
        year: '',
      },
      weekArr,
    }
  },
  computed: {
    secondsText() {
      let seconds = ''
      let cronEvery = this.second.cronEvery
      switch (cronEvery.toString()) {
        case '1':
          seconds = '*'
          break
        case '2':
          seconds = this.second.rangeStart + '-' + this.second.rangeEnd
          break
        case '3':
          seconds = this.second.intervalStart + '/' + this.second.interval
          break
        case '4':
          seconds = this.second.specifics.join(',')
          break
        default:
          seconds = '*'
          break
      }
      return seconds
    },
    minutesText() {
      let minutes = ''
      let cronEvery = this.minute.cronEvery
      switch (cronEvery.toString()) {
        case '1':
          minutes = '*'
          break
        case '2':
          minutes = this.minute.rangeStart + '-' + this.minute.rangeEnd
          break
        case '3':
          minutes = this.minute.intervalStart + '/' + this.minute.interval
          break
        case '4':
          minutes = this.minute.specifics.join(',')
          break
        default:
          minutes = '*'
          break
      }
      return minutes
    },
    hoursText() {
      let hours = ''
      let cronEvery = this.hour.cronEvery
      switch (cronEvery.toString()) {
        case '1':
          hours = '*'
          break
        case '2':
          hours = this.hour.rangeStart + '-' + this.hour.rangeEnd
          break
        case '3':
          hours = this.hour.intervalStart + '/' + this.hour.interval
          break
        case '4':
          hours = this.hour.specifics.join(',')
          break
        default:
          hours = '*'
          break
      }
      return hours
    },
    daysText() {
      let days = ''
      let cronEvery = this.day.cronEvery
      switch (cronEvery.toString()) {
        case '1':
          days = '*'
          break
        case '2':
          days = '?'
          break
        case '3':
          days = this.day.rangeStart + '-' + this.day.rangeEnd
          break
        case '4':
          days = this.day.intervalStart + '/' + this.day.interval
          break
        case '5':
          days = this.day.specificW + 'W'
          break
        case '6':
          days = 'L'
          break
        case '7':
          days = this.day.specifics.join(',')
          break
        default:
          days = '*'
          break
      }
      return days
    },
    monthsText() {
      let months = ''
      let cronEvery = this.month.cronEvery
      switch (cronEvery.toString()) {
        case '1':
          months = '*'
          break
        case '2':
          months = '?'
          break
        case '3':
          months = this.month.rangeStart + '-' + this.month.rangeEnd
          break
        case '4':
          months = this.month.intervalStart + '/' + this.month.interval
          break
        case '5':
          months = this.month.specifics.join(',')
          break
        default:
          months = '*'
          break
      }
      return months
    },
    weeksText() {
      let weeks = ''
      let cronEvery = this.week.cronEvery
      switch (cronEvery.toString()) {
        case '1':
          weeks = '*'
          break
        case '2':
          weeks = '?'
          break
        case '3':
          weeks = this.week.rangeStart + '-' + this.week.rangeEnd
          break
        case '4':
          weeks = this.week.specific + '#' + this.week.specificDay
          break
        case '5':
          weeks = this.week.lastWeek + 'L'
          break
        case '6':
          weeks = this.week.specifics.join(',')
          break
        default:
          weeks = '*'
          break
      }
      return weeks
    },
    yearsText() {
      let years = ''
      let cronEvery = this.year.cronEvery
      switch (cronEvery.toString()) {
        case '1':
          years = '*'
          break
        case '2':
          years = ''
          break
        case '3':
          years = this.year.rangeStart + '-' + this.year.rangeEnd
          break
        default:
          years = ''
          break
      }
      return years
    },
    cron() {
      return `${this.secondsText || '*'} ${this.minutesText || '*'} ${this
        .hoursText || '*'} ${this.daysText || '*'} ${this.monthsText ||
        '*'} ${this.weeksText || '*'}${' ' + this.yearsText || ''}`
    },
  },
  watch: {
    // data() {
    //   this.rest(this.$data)
    // },
    cron(newVal) {
      this.$emit('update:value', newVal)
    },
  },
  mounted() {
    this.initCron(this.data || this.value)
  },
  methods: {
    parseCron(reg, index) {
      switch (index) {
        case 0:
          this.initSMH(reg, 'second')
          break
        case 1:
          this.initSMH(reg, 'minute')
          break
        case 2:
          this.initSMH(reg, 'hour')
          break
        case 3:
          this.initDay(reg)
          break
        case 4:
          this.initMouth(reg)
          break
        case 5:
          this.initWeek(reg)
          break
        case 6:
          this.initYear(reg)
          break
        default:
          break
      }
    },
    /**
     * reg: string
     * type: 'second' | 'minute' | 'hour'
     */
    initSMH(reg, type) {
      if (reg === '*') {
        this[type].cronEvery = '1'
      } else if (reg.includes('-')) {
        let arr = reg.split('-')
        this[type].rangeStart = arr[0]
        this[type].rangeEnd = arr[1]
        this[type].cronEvery = '2'
      } else if (reg.includes('/')) {
        let arr = reg.split('/')
        this[type].intervalStart = arr[0]
        this[type].interval = arr[1]
        this[type].cronEvery = '3'
      } else {
        let arr = reg.split(',')
        this[type].specifics = arr
        this[type].cronEvery = '4'
      }
    },

    initDay(reg) {
      if (reg === '*') {
        this.day.cronEvery = '1'
      } else if (reg === '?') {
        this.day.cronEvery = '2'
      } else if (reg === 'L') {
        this.day.cronEvery = '6'
      } else if (reg.includes('-')) {
        let arr = reg.split('-')
        this.day.rangeStart = arr[0]
        this.day.rangeEnd = arr[1]
        this.day.cronEvery = '3'
      } else if (reg.includes('/')) {
        let arr = reg.split('/')
        this.day.intervalStart = arr[0]
        this.day.interval = arr[1]
        this.day.cronEvery = '4'
      } else if (reg.includes('W')) {
        let arr = reg.split('W')
        this.day.specificW = arr[0]
        this.day.cronEvery = '5'
      } else {
        this.day.specifics = reg.split(',')
        this.cronEvery = '7'
      }
    },
    initMouth(reg) {
      if (reg === '*') {
        this.month.cronEvery = '1'
      } else if (reg === '?') {
        this.month.cronEvery = '2'
      } else if (reg.includes('-')) {
        let arr = reg.split('-')
        this.month.rangeStart = arr[0]
        this.month.rangeEnd = arr[1]
        this.month.cronEvery = '3'
      } else if (reg.includes('/')) {
        let arr = reg.split('/')
        this.month.intervalStart = arr[0]
        this.month.interval = arr[1]
        this.month.cronEvery = '4'
      } else {
        let arr = reg.split(',')
        this.month.specifics = arr
        this.month.cronEvery = '5'
      }
    },
    initWeek(reg) {
      if (reg === '*') {
        this.week.cronEvery = '1'
      } else if (reg === '?') {
        this.week.cronEvery = '2'
      } else if (reg.includes('-')) {
        let arr = reg.split('-')
        this.week.rangeStart = arr[0]
        this.week.rangeEnd = arr[1]
        this.week.cronEvery = '3'
      } else if (reg.includes('#')) {
        let arr = reg.split('#')
        this.week.specific = arr[0]
        this.week.specificDay = arr[1]
        this.week.cronEvery = '4'
      } else if (reg.includes('L')) {
        let arr = reg.split('L')
        this.week.lastWeek = arr[0]
        this.week.cronEvery = '5'
      } else {
        let arr = reg.split(',')
        this.week.specifics = arr
        this.week.cronEvery = '6'
      }
    },
    initYear(reg) {
      if (!reg) {
        this.year.cronEvery = '2'
      } else if (reg === '*') {
        this.year.cronEvery = '1'
      } else {
        let arr = reg.split('-')
        this.year.rangeStart = arr[0]
        this.year.rangeEnd = arr[1]
        this.year.cronEvery = '3'
      }
    },
    initCron(reg) {
      let data = reg || this.data || '* * * * * *'
      let regs = data.split(' ')
      regs.map((reg, index) => {
        this.parseCron(reg, index)
      })
    },
    getValue() {
      return this.cron
    },
    change() {
      this.$emit('change', this.cron)
      this.close()
    },
    close() {
      this.$emit('close')
    },
    rest(data) {
      for (let i in data) {
        if (data[i] instanceof Object) {
          this.rest(data[i])
        } else {
          switch (typeof data[i]) {
            case 'object':
              data[i] = []
              break
            case 'string':
              data[i] = ''
              break
          }
        }
      }
    },
  },
}
</script>
