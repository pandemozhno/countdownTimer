<template>
  <div id="app">
    <div class="header">
      <input type="number" v-model="nextTimerTime"/>
      <button @click="setTimer">add countdown timer</button>
    </div>

    <div class="timers-list">
      <template v-for="time, index in timers" >
        <div class="timers-list__item"
          :key="index"
        >
          <span>#{{ index + 1 }} :&nbsp;</span>
          <CountdownTimer
            
            :seconds="time"
            @done="finishHandler($event, index)"
          />
        </div>
      </template>
    </div>

    <div class="timers-finish">
      <div v-for="time, key in finishTimes" :key="'f' + key">
        #{{ key }} : {{ time }}
      </div>
    </div>
  </div>
</template>

<script>
import CountdownTimer from './components/CountdownTimer'

export default {
  name: 'app',
  components: {
    CountdownTimer
  },
  data () {
    return {
      nextTimerTime: 10,
      timers: [],
      finishTimes: {}
    }
  },
  methods: {
    setTimer () {
      this.timers.push(this.nextTimerTime)
    },
    finishHandler (finishTime, number) {
      this.$set(this.finishTimes, number + 1, finishTime)
    }
  }
}
</script>

<style>
#app {
  display: flex;
  width: 100%;
  max-width: 520px;
  flex-direction: column;
  margin: auto;
  background-color: #eee;
  padding: 10px;
  height: auto;
  min-height: 400px;
}
.timers-list__item {
  display: flex;
}
.timers-finish {
  background-color: #ddd;
  margin-top: 20px;
  padding: 5px;
  font-size: 10px;
}
</style>
