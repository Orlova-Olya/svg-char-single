<template>
  <svg v-if="isValidProps" :width="sideLength" :height="sideLength" class="svg-char">
    <!--↓ ring - кольцо-фон ↓-->
    <circle
      :r="radius"
      :cx="sideLength / 2"
      :cy="sideLength / 2"
      :stroke-width="ringWidth"
      :stroke="ringColor"
      fill="none"
    />
    <!--↓ arc - дуга ↓-->
    <circle
      :r="radius"
      :cx="sideLength / 2"
      :cy="sideLength / 2"
      :stroke-width="arcWidth"
      :stroke-dasharray="arcStrokeDasharray"
      :stroke="arcColor"
      :stroke-linecap="arcStrokeLinecap"
      fill="none"
      class="svg-char__arc"
    />
  </svg>
  <p v-else>
    <i>ringWidth</i>
    и
    <i>arcWidth</i>
    должны быть не более половины от
    <i>sideLength</i>
  </p>
</template>

<script>
export default {
  name: 'SVGChar',
  props: {
    sideLength: {
      type: Number,
      default: 100,
      validator(value) {
        return value > 0
      }
    },
    ringWidth: {
      type: Number,
      default: 15,
      validator(value) {
        return value > 0
      }
    },
    ringColor: {
      type: String,
      default: 'transparent',
      validator(value) {
        return /^#([0-9A-F]{3}){1,2}$/i.test(value)
      }
    },
    arcWidth: {
      type: Number,
      default: 15,
      validator(value) {
        return value > 0
      }
    },
    arcColor: {
      type: String,
      default: '#2aa6dc',
      validator(value) {
        return /^#([0-9A-F]{3}){1,2}$/i.test(value)
      }
    },
    arcStrokeLinecap: {
      type: String,
      default: 'butt',
      validator(value) {
        return ['butt', 'square', 'round'].includes(value)
      }
    },
    percentage: {
      type: Number,
      required: true,
      validator(value) {
        return value >= 0 && value <= 100
      }
    }
  },
  computed: {
    isValidProps() {
      return this.sideLength / 2 >= this.ringWidth && this.sideLength / 2 >= this.arcWidth
    },
    radius() {
      const widestCircleWidth = this.ringWidth > this.arcWidth ? this.ringWidth : this.arcWidth
      return this.sideLength / 2 - widestCircleWidth / 2
    },
    arcStrokeDasharray() {
      const circumference = 2 * Math.PI * this.radius //Длина окружности
      return (circumference * this.percentage) / 100 + ', ' + circumference
    }
  }
}
</script>

<style lang="scss">
.svg-char {
  transform: rotate(-90deg);
  transform-origin: center;

  &__arc:hover {
    stroke: pink;
  }
}
</style>
