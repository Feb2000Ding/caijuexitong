<!--<template>-->

<!--</template>-->

<!--<script>-->
<!--export default {-->
<!--  name: "RenderText.vue"-->
<!--}-->
<!--</script>-->

<!--<style scoped>-->

<!--</style>-->

<template>
  <div></div>
</template>

<script setup lang="ts">
import { Text } from 'leafer-ui'

defineProps({
  text: {
    type: String,
    required: true
  },
  x: {
    type: Number,
    default: 0
  },
  y: {
    type: Number,
    default: 0
  },
  fontSize: {
    type: Number,
    default: 16
  },
  fill: {
    type: String,
    default: '#FFFFFF'
  }
})

const props = defineProps()

onMounted(() => {
  const textElement = new Text({
    fill: props.fill,
    fontSize: props.fontSize,
    text: props.text,
    x: props.x,
    y: props.y
  })

  leafer.tree.add(textElement)
})
</script>

<style scoped>
/* Scoped styles can be added here if needed */
</style>
