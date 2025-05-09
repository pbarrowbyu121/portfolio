<template>
  <div class="film-wheel-container">
    <h1>Film Wheel</h1>

    <div class="picker-container">
      <div class="picker">
        <!-- Top and bottom gradients to create wheel illusion -->
        <div class="picker-gradient-top"></div>
        <div class="picker-gradient-bottom"></div>

        <!-- Center highlighted area -->
        <div class="picker-center-line"></div>

        <!-- The scrolling film list -->
        <div
          class="picker-items"
          :style="{ transform: `translateY(${position}px)` }"
        >
          <div
            v-for="(film, index) in displayFilms"
            :key="index"
            class="picker-item"
          >
            {{ film.title }}
          </div>
        </div>
      </div>
    </div>

    <button class="spin-button" :disabled="isSpinning" @click="spinWheel">
      {{ isSpinning ? 'Spinning...' : 'Spin' }}
    </button>
  </div>
</template>

<script>
// Import films from the JSON file
import filmsData from '@/assets/data/films.json'

export default {
  data() {
    return {
      films: filmsData,
      position: 0,
      itemHeight: 50, // Height of each film item
      isSpinning: false,
      spinInterval: null,
      animationFrame: null,
      // Create a repeated list for continuous scrolling effect
      displayFilms: [],
      lastEndPosition: null, // Track the last ending position
    }
  },
  mounted() {
    // Create a repeated list for seamless infinite scrolling
    // We need to duplicate the list several times to ensure we have enough items for continuous scrolling
    this.displayFilms = [
      ...this.films,
      ...this.films,
      ...this.films,
      ...this.films,
    ]

    // Initialize position to show the second set of films
    // This way we can scroll up or down and still have items to display
    this.position = -(this.films.length * this.itemHeight)
  },
  beforeDestroy() {
    this.cleanupAnimation()
  },
  methods: {
    spinWheel() {
      if (this.isSpinning) return

      this.isSpinning = true
      this.cleanupAnimation() // Clean up any existing animation

      // Generate truly random animation parameters
      // Longer animation duration (5-8 seconds) for more suspense
      const duration = 5000 + Math.random() * 3000
      // Random initial speed (affects total distance traveled)
      const initialSpeed = 20 + Math.random() * 15 // between 20-35

      const startTime = performance.now()
      let currentSpeed = initialSpeed

      // Add a random offset at the beginning to avoid patterns
      this.position -= Math.random() * this.itemHeight

      // Animation function using requestAnimationFrame for smooth motion
      const animate = (timestamp) => {
        // Calculate progress through the animation (0 to 1)
        const elapsed = timestamp - startTime
        const progress = Math.min(elapsed / duration, 1)

        // Start slowing down earlier but make it much more gradual
        // Begin deceleration at around 30% of the animation
        const decelerationStartPoint = 0.3 + Math.random() * 0.1

        if (progress > decelerationStartPoint) {
          // Map progress from deceleration point to 1.0
          const easingProgress =
            (progress - decelerationStartPoint) / (1 - decelerationStartPoint)

          // Use a more gradual power curve for deceleration
          // Higher power = more gradual initial slowdown with dramatic final slowdown
          // This creates more suspense as the wheel seems like it might keep going
          const easeOut = 1 - Math.pow(easingProgress, 2.5)

          // Apply the easing to the speed, but keep a minimum speed until very end
          // This prevents it from slowing down too quickly
          const minSpeedFactor = Math.max(0.2, 1 - easingProgress * 1.5)
          currentSpeed = Math.max(
            initialSpeed * easeOut,
            initialSpeed * 0.15 * minSpeedFactor
          )

          // Add slight "tension" effect near the end - the wheel briefly resists stopping
          // This creates an effect like the wheel is about to stop but keeps going a bit longer
          if (easingProgress > 0.7 && easingProgress < 0.9) {
            currentSpeed *=
              1 + Math.sin((easingProgress - 0.7) * Math.PI * 5) * 0.1
          }
        }

        // Move the wheel
        this.position -= currentSpeed

        // Check if we've scrolled too far and need to reset
        // const totalHeight = this.films.length * this.itemHeight
        if (
          Math.abs(this.position) >=
          (this.displayFilms.length - this.films.length) * this.itemHeight
        ) {
          // Reset to the position of the second set of films
          this.position = -(this.films.length * this.itemHeight)
        }

        // Continue animation if not complete
        if (progress < 1) {
          this.animationFrame = requestAnimationFrame(animate)
        } else {
          // Ensure we don't stop at the same spot as last time
          // if (this.lastEndPosition !== null) {
          //   const currentMod = this.position % totalHeight
          //   const lastMod = this.lastEndPosition % totalHeight

          //   // If we're too close to the last position, add a random offset
          //   if (Math.abs(currentMod - lastMod) < this.itemHeight * 2) {
          //     this.position -=
          //       this.itemHeight * (2 + Math.floor(Math.random() * 3))
          //   }
          // }

          // End of animation - snap to nearest item
          this.lastEndPosition = this.position
          this.snapToNearestItem()
          this.isSpinning = false
        }
      }

      // Start the animation
      this.animationFrame = requestAnimationFrame(animate)
    },

    // New method to snap the film to the center of the highlighted area
    snapToNearestItem() {
      // Calculate which item position is closest to the center
      // First, find where the midpoint of the picker is in relation to our items
      const centerOffset = this.position % this.itemHeight
      let adjustment = 0

      // If we're more than halfway through an item, snap forward
      // otherwise snap backwards to center the item
      if (Math.abs(centerOffset) > this.itemHeight / 2) {
        // Adjust to next item
        adjustment =
          centerOffset > 0
            ? this.itemHeight - Math.abs(centerOffset)
            : -(this.itemHeight - Math.abs(centerOffset))
      } else {
        // Adjust to center current item
        adjustment = -centerOffset
      }

      // Create a smooth animation to center the item
      const startPosition = this.position
      const targetPosition = this.position + adjustment
      const duration = 300 // Short duration for the snap
      const startTime = performance.now()

      const animateSnap = (timestamp) => {
        const elapsed = timestamp - startTime
        const progress = Math.min(elapsed / duration, 1)

        // Use an easeOutQuad function for smooth snapping
        const easeOut = 1 - Math.pow(1 - progress, 2)

        // Update position
        this.position = startPosition + adjustment * easeOut

        if (progress < 1) {
          requestAnimationFrame(animateSnap)
        } else {
          // Ensure we end exactly at the target position
          this.position = targetPosition
        }
      }

      requestAnimationFrame(animateSnap)
    },

    cleanupAnimation() {
      // Clean up any existing animations
      if (this.animationFrame) {
        cancelAnimationFrame(this.animationFrame)
        this.animationFrame = null
      }

      if (this.spinInterval) {
        clearInterval(this.spinInterval)
        this.spinInterval = null
      }
    },
  },
}
</script>

<style scoped>
.film-wheel-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.picker-container {
  margin: 40px 0;
  width: 100%;
  max-width: 400px;
}

.picker {
  position: relative;
  height: 250px;
  overflow: hidden;
  border-radius: 10px;
  background-color: #f5f5f7;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.picker-items {
  /* Disable transition so we can control animation precisely */
  transition: none;
  /* Extra padding to ensure items appear to come from off-screen */
  padding: 100px 0;
}

.picker-item {
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  font-weight: bold;
  color: #555;
  padding: 0 20px;
  text-align: center;
}

.picker-gradient-top {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100px;
  background: linear-gradient(
    to bottom,
    rgba(245, 245, 247, 1) 20%,
    rgba(245, 245, 247, 0)
  );
  z-index: 2;
  pointer-events: none;
}

.picker-gradient-bottom {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100px;
  background: linear-gradient(
    to top,
    rgba(245, 245, 247, 1) 20%,
    rgba(245, 245, 247, 0)
  );
  z-index: 2;
  pointer-events: none;
}

.picker-center-line {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  height: 50px;
  margin-top: -25px;
  background-color: rgba(0, 0, 0, 0.05);
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  z-index: 1;
  pointer-events: none;
}

.spin-button {
  margin-top: 20px;
  padding: 12px 24px;
  font-size: 18px;
  font-weight: bold;
  background-color: #e74c3c;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.spin-button:hover:not(:disabled) {
  background-color: #c0392b;
  transform: scale(1.05);
}

.spin-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
