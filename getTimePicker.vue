<template>
  <section class="container">
    <div>
      <h1>{{ $t('labels.about') }}</h1>
      <div>
        <el-radio-group v-model="radio1" @change="getPicker">
          <el-radio-button :label="1">1天</el-radio-button>
          <el-radio-button :label="2">2</el-radio-button>
          <el-radio-button :label="3">3</el-radio-button>
          <el-radio-button :label="4">4</el-radio-button>
        </el-radio-group>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      radio1: 1
    }
  },
  methods: {
    getPicker () {
      // const start = new Date()
      const day = this.radio1
      const letday = this.getRecentDate(day)
      console.log(letday)
    },
    getRecentDate (num) {
      let day = num || 30
      // let day = this.radio1
      let curDateStamp = new Date().getTime()
      let recentDateStamp = day * 24 * 60 * 60 * 1000
      let prevDate = new Date(curDateStamp - recentDateStamp)
      console.log(prevDate)
      let formatDate = prevDate.getFullYear() + '-' + ((prevDate.getMonth() + 1).toString().length === 1 ? '0' + (prevDate.getMonth() + 1).toString() : (prevDate.getMonth() + 1).toString()) + '-' + (prevDate.getDate().toString().length === 1 ? '0' + prevDate.getDate().toString() : prevDate.getDate().toString())
      return formatDate
    }
  }
}
</script>
