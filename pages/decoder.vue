<template>
  <div class="flex justify-center">
    <div>
      <TreasureHuntInstructions />
      <div class="flex justify-center">
        <Decoder />
      </div>
      <template v-if="isBeforeSevenPM">
        <div class="flex justify-center mx-auto mb-4">
          <Countdown />
        </div>
      </template>

      <div class="p-4">
        <img src="../assets/images/IMG_4513.jpg" />
      </div>

      <TreasureHuntImages />
    </div>
  </div>
</template>

<script>
import Decoder from '../components/Decoder.vue'
import TreasureHuntInstructions from '../components/TreasureHuntInstructions.vue'
import TreasureHuntImages from '../components/TreasureHuntImages.vue'
import Countdown from '../components/Countdown.vue'
export default {
  components: {
    Decoder,
    TreasureHuntInstructions,
    TreasureHuntImages,
    Countdown,
  },
  data() {
    return {
      column: '',
      row: null,
      result: null,
      now: new Date(),
    }
  },
  computed: {
    isBeforeSevenPM() {
      const now = new Date()

      // Calculate the date and time for Monday, the 19th at 7:00 PM
      const targetDate = new Date(
        now.getFullYear(),
        now.getMonth(),
        now.getDate(),
        19,
        0,
        0
      )

      // Calculate the number of days until next Monday
      const daysUntilNextMonday = (8 - now.getDay()) % 7 // Days until next Monday

      // If today is Monday and the time is past 7:00 PM, we need to set the target to the next Monday
      if (now.getDay() === 1 && now.getHours() >= 19) {
        targetDate.setDate(now.getDate() + 7) // Move to the next Monday
      } else {
        targetDate.setDate(now.getDate() + daysUntilNextMonday)
      }

      return now < targetDate
    },
  },
  created() {
    // Update time every second
    this.timer = setInterval(this.updateNow, 1000)
  },
  beforeDestroy() {
    // Clear timer on component destroy
    clearInterval(this.timer)
  },
  methods: {
    updateNow() {
      this.now = new Date()
    },
  },
}
</script>

<style scoped></style>
