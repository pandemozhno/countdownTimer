<template>
  <div class="countdown-timer">
    <div class="countdown-timer__digits">{{ countdownValue }}</div>
  </div>
</template>

<script>
export default {
  name: 'CountdownTimer',
  props: {
    seconds: {
      type: [Number, String],
      default: 10
    }
  },
  data () {
    return {
      finish: false,
      countdownValue: null
    }
  },
  mounted () {
    this.startCountdown()
  },
  methods: {
    startCountdown () {
      const waitMoment = () => new Promise(resolve => setTimeout(resolve, 1));
      var ms = this.seconds * 1000
      let asyncInterval = new Promise((resolve) => {
        (async () => {
          let prevTimestamp = Date.now()
          let now, current
          do {
            await waitMoment()
            now = Date.now()
            current = ((ms - (now - prevTimestamp)) / 1000).toFixed(3)
            if (current < 0) this.countdownValue = '00.000'
            else {
              if (current.toString().length < 6) this.countdownValue = `0${current}`
              else this.countdownValue = current
            }
          } while ( now - prevTimestamp < ms )
            resolve(new Date())
        })()
      })

      asyncInterval.then(res => this.$emit('done', res))
    }
  }
}
</script>

<style>
</style>
