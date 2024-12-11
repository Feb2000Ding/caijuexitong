<script setup lang="ts">
import RenderImages from './components/RenderImages.vue'
</script>

<template>
  <RenderImages />
</template>

<style scoped>

</style>
<!--<script setup lang="ts">-->
<!--import { onMounted, reactive } from 'vue'-->
<!--import { App } from 'leafer-ui'-->
<!--import ImageComponent from './components/RenderImages.vue'-->
<!--import TextComponent from './components/RenderText.vue'-->

<!--const state = reactive({-->
<!--  currentTime: new Date().toLocaleString()-->
<!--})-->

<!--const images = [-->
<!--  { url: '/assets/newImages/u1.png', width: 1920, height: 1080, x: 0, y: 0 },-->
<!--  { url: '/assets/images/u24.png', width: 1860 * 0.75, height: 49 * 0.75, x: 0, y: 1040 },-->
<!--  { url: '/assets/images/u348.png', width: 1920 * 0.75, height: 129 * 0.75, x: 0, y: 0 },-->
<!--  { url: '/assets/images/u23.png', width: 43 * 0.75, height: 645 * 0.75, x: 0, y: 200 },-->
<!--  { url: '/assets/images/u22.png', width: 43 * 0.75, height: 645 * 0.75, x: 1877, y: 200 }-->
<!--]-->

<!--const texts = [-->
<!--  { text: state.currentTime, x: 100, y: 20, fontSize: 16, fill: '#F2F3FA' },-->
<!--  { text: '裁决及效果模拟软件', x: 700, y: 35, fontSize: 24, fill: '#F2F3FA' }-->
<!--]-->

<!--let leafer: App;-->

<!--onMounted(() => {-->
<!--  leafer = new App({ view: 'leafer-view', fill: '#242424', editor: {} })-->
<!--})-->
<!--</script>-->

<!--<template>-->
<!--  <div id="leafer-view">-->
<!--    <ImageComponent-->
<!--        v-for="(image, index) in images"-->
<!--        :key="index"-->
<!--        :leafer="leafer"-->
<!--    :imageUrl="image.url"-->
<!--    :width="image.width"-->
<!--    :height="image.height"-->
<!--    :x="image.x"-->
<!--    :y="image.y"-->
<!--    />-->
<!--    <TextComponent-->
<!--        v-for="(text, index) in texts"-->
<!--        :key="index"-->
<!--        :text="text.text"-->
<!--        :x="text.x"-->
<!--        :y="text.y"-->
<!--        :fontSize="text.fontSize"-->
<!--        :fill="text.fill"-->
<!--    />-->
<!--  </div>-->
<!--</template>-->


