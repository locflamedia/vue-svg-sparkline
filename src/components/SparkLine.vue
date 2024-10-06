<template>
  <svg
    :class="{ 'fade-in': isVisible }"
    :style="`background-color: ${backgroundColor}; margin: 0; padding: 0; box-sizing: border-box;`"
    :width="width"
    :height="height"
    :viewBox="`0 0 ${width} ${height}`"
  >
    <path
      :d="[shape, fillEndPath].join(' ')"
      :fill="fill"
      :style="`opacity: ${opacity / 100};`"
    ></path>

    <path
      :d="shape"
      fill="none"
      :stroke="strokeColor"
      :stroke-width="stroke"
    ></path>
  </svg>
</template>

<script setup>
import { computed, toRefs, defineProps } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    default: () => [],
  },
  width: {
    type: Number,
    default: 100,
  },
  height: {
    type: Number,
    default: 20,
  },
  stroke: {
    type: Number,
    default: 1,
  },
  strokeColor: {
    type: String,
    default: '#000000',
  },
  fill: {
    type: String,
    default: '#000000',
  },
  backgroundColor: {
    type: String,
    default: '#ffffff',
  },
  opacity: {
    type: Number, // 1 - 100
    default: 10,
  },
  centerOffset: {
    type: Number,
    default: 2,
  },
  amplitudeFactor: {
    type: Number,
    default: 5,
  },
  highestPoint: {
    type: Number,
    default: null,
  },
})

const {
  data,
  width,
  height,
  fill,
  backgroundColor,
  opacity,
  stroke,
  centerOffset,
  amplitudeFactor,
  highestPoint,
} = toRefs(props)

const shape = computed(() => {
  const heightValue = height.value
  const dataArray = data.value || []

  const average = dataArray.length
    ? dataArray.reduce((acc, val) => acc + val, 0) / dataArray.length
    : 0

  const normalizedData = dataArray.map((item) => item - average)
  const maxPoint =
    highestPoint.value !== null
      ? highestPoint.value
      : Math.max(...normalizedData) || 1
  const coordinates = []
  const totalPoints = dataArray.length - 1

  normalizedData.forEach((item, n) => {
    const x = (n / totalPoints) * width.value
    const y =
      heightValue / centerOffset.value -
      (item / maxPoint) * (heightValue / amplitudeFactor.value)

    coordinates.push({ x, y })
  })

  const path = coordinates.length
    ? coordinates
        .map((point, i) => `${i === 0 ? 'M' : 'L'} ${point.x} ${point.y}`)
        .join(' ')
    : `M 0 ${heightValue / centerOffset.value} L ${width.value} ${
        heightValue / amplitudeFactor.value
      }`

  return path
})

const fillEndPath = computed(() => {
  const lastX = width.value
  const lastY = height.value

  return `L ${lastX} ${lastY} L 0 ${lastY} Z`
})
</script>

<style scoped>
.fade-in {
  opacity: 0;
  animation: fadeIn 0.6s forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
