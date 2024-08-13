<template>
  <div class="flex flex-col justify-center items-center">
    <div>The hunt begins in:</div>
    <span>{{ timeLeft }}</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timer: null,
      endTime: null,
      timeLeft: '00:00:00:00', // Format DD:hh:mm:ss
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
        end.setDate(end.getDate() + 7) // Move to the same time next week
      } else {
        // If the end time is in the future, set it for next week
        end.setDate(end.getDate() + (7 - now.getDay())) // Move to next Monday
      }
      this.endTime = end
      this.updateCountdown()
      this.timer = setInterval(this.updateCountdown, 1000)
    },
    updateCountdown() {
      const now = new Date()
      const diff = this.endTime - now
      if (diff <= 0) {
        this.timeLeft = '00:00:00:00'
        clearInterval(this.timer)
        return
      }
      const days = Math.floor(diff / (1000 * 60 * 60 * 24))
      const hours = Math.floor(
        (diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
      )
      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))
      const seconds = Math.floor((diff % (1000 * 60)) / 1000)
      this.timeLeft = this.formatTime(days, hours, minutes, seconds)
    },
    formatTime(days, hours, minutes, seconds) {
      const pad = (n) => (n < 10 ? '0' : '') + n
      return `${pad(days)}:${pad(hours)}:${pad(minutes)}:${pad(seconds)}`
    },
  },
}
</script>

<style scoped>
/* Add styles here if needed */
</style>
