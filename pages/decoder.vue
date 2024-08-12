<template>
  <div class="flex justify-center">
    <div>
      <TreasureHuntInstructions />
      <div class="flex justify-center">
        <Decoder />
      </div>
      <template v-if="isBeforeSevenPM">
        <div class="flex justify-center mx-auto">
          <Countdown />
        </div>
      </template>
      <template v-else>
        <div class="p-4">
          <img src="../assets/images/IMG_4513.jpg" />
        </div>

        <TreasureHuntImages />
      </template>
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
      // Get current time
      const now = new Date()
      // Create end time (7:00 PM MST)
      const end = new Date(
        now.getFullYear(),
        now.getMonth(),
        now.getDate(),
        19,
        0,
        0
      )

      // Adjust for MST if needed (assuming the local time is MST)
      // Convert to milliseconds since epoch for comparison
      return now < end
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
