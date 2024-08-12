<template>
  <div class="flex flex-col justify-center items-center">
    <div>Time remaining:</div>
    <span>{{ timeLeft }}</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timer: null,
      endTime: null,
      timeLeft: '00:00:00',
    }
  },
  created() {
    this.initializeCountdown()
  },
  beforeDestroy() {
    clearInterval(this.timer)
  },
  methods: {
    initializeCountdown() {
      const now = new Date()
      const end = new Date(
        now.getFullYear(),
        now.getMonth(),
        now.getDate(),
        19,
        0,
        0
      ) // 7:00 PM
      if (now > end) {
        end.setDate(end.getDate() + 1) // Move to the next day if the time has already passed
      }
      this.endTime = end
      this.updateCountdown()
      this.timer = setInterval(this.updateCountdown, 1000)
    },
    updateCountdown() {
      const now = new Date()
      const diff = this.endTime - now
      if (diff <= 0) {
        this.timeLeft = '00:00:00'
        clearInterval(this.timer)
        return
      }
      const hours = Math.floor(diff / (1000 * 60 * 60))
      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))
      const seconds = Math.floor((diff % (1000 * 60)) / 1000)
      this.timeLeft = this.formatTime(hours, minutes, seconds)
    },
    formatTime(hours, minutes, seconds) {
      const pad = (n) => (n < 10 ? '0' : '') + n
      return `${pad(hours)}:${pad(minutes)}:${pad(seconds)}`
    },
  },
}
</script>

<style scoped>
/* Add styles here if needed */
</style>
