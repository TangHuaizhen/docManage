<template>
  <section class="container">
    <div>
      <h1>{{ $t('labels.about') }}</h1>
      <el-date-picker
        ref="datepickerDemo"
        v-model="value1"
        type="datetimerange"
        format="yyyy/MM/dd HH:mm"
        value-format="yyyy/MM/dd HH:mm"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
        style="visibility: hidden;"
        @change="realTimeFn">
      </el-date-picker>
      <h2 style="position: absolute;top: 100px;">{{ pickerDate }}</h2>
      <div>
        <el-radio-group v-model="radio1" @change="getPicker">
          <el-radio-button :label="1">1天</el-radio-button>
          <el-radio-button :label="2">2</el-radio-button>
          <el-radio-button :label="3">3</el-radio-button>
          <el-radio-button :label="4">4</el-radio-button>
          <el-radio-button label="自定义">自定义</el-radio-button>
        </el-radio-group>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      radio1: 1,
      value1: '',
      pickerDate: ''
    }
  },
  methods: {
    realTimeFn () {
      this.pickerDate = this.value1[0]
    },
    getPicker () {
      if (this.radio1 === '自定义') {
        this.$refs['datepickerDemo'].focus()
        this.radio1 = ''
      } else {
        // const start = new Date()
        const day = this.radio1
        const letday = this.getRecentDate(day)
        console.log(letday)
      }
    },
    getRecentDate (num) {
      let day = num || 30
      // let day = this.radio1
      let curDateStamp = new Date().getTime()
      let recentDateStamp = day * 24 * 60 * 60 * 1000
      let prevDate = new Date(curDateStamp - recentDateStamp)
      console.log(prevDate)
      this.pickerDate = prevDate.toLocaleDateString()
      let formatDate = prevDate.getFullYear() + '-' + ((prevDate.getMonth() + 1).toString().length === 1 ? '0' + (prevDate.getMonth() + 1).toString() : (prevDate.getMonth() + 1).toString()) + '-' + (prevDate.getDate().toString().length === 1 ? '0' + prevDate.getDate().toString() : prevDate.getDate().toString())
      return formatDate
    }
  }
}
</script>
