<!--<script setup lang="ts">-->
<!--import { onMounted } from 'vue'-->
<!--import { Rect } from 'leafer-ui'-->

<!--defineProps({-->
<!--  leafer: {-->
<!--    type: Object,-->
<!--    required: true-->
<!--  },-->
<!--  imageUrl: {-->
<!--    type: String,-->
<!--    required: true-->
<!--  },-->
<!--  width: {-->
<!--    type: Number,-->
<!--    default: 1920-->
<!--  },-->
<!--  height: {-->
<!--    type: Number,-->
<!--    default: 1080-->
<!--  },-->
<!--  x: {-->
<!--    type: Number,-->
<!--    default: 0-->
<!--  },-->
<!--  y: {-->
<!--    type: Number,-->
<!--    default: 0-->
<!--  }-->
<!--})-->

<!--const props = defineProps()-->

<!--const loadImage = (url: string): Promise<HTMLImageElement> => {-->
<!--  return new Promise((resolve, reject) => {-->
<!--    const img = new Image()-->
<!--    img.src = url-->
<!--    img.onload = () => resolve(img)-->
<!--    img.onerror = reject-->
<!--  })-->
<!--}-->

<!--onMounted(async () => {-->
<!--  await loadImage(props.imageUrl)-->

<!--  const image = new Rect({-->
<!--    width: props.width,-->
<!--    height: props.height,-->
<!--    x: props.x,-->
<!--    y: props.y,-->
<!--    fill: {-->
<!--      type: 'image',-->
<!--      url: props.imageUrl,-->
<!--      mode: 'cover'-->
<!--    }-->
<!--  })-->

<!--  // 使用传入的 leafer 实例-->
<!--  props.leafer.tree.add(image)-->
<!--})-->
<!--</script>-->

<script setup lang="ts">
import { onMounted, reactive } from 'vue'
import { App, Rect, Text, Group } from 'leafer-ui'
import 'leafer-editor'
import '@leafer-in/state'
import { Flow } from '@leafer-in/flow'

// Vue reactive 数据，用来存储时间
const state = reactive({
  currentTime: new Date().toLocaleString()
})

// 每秒更新时间
setInterval(() => {
  state.currentTime = new Date().toLocaleString()
}, 1000)

onMounted(() => {
  const leafer = new App({ view: 'leafer-view', fill: '#242424', editor: {} })
  const { width = 1920, height = 1080 } = leafer

  // 静态背景图
  const backgroundImage = new Rect({
    width: width,
    height: height,
    fill: {
      type: 'image',
      url: '/assets/newImages/u1.png',
      mode: 'cover'
    }
  })
  leafer.tree.add(backgroundImage)

  // 底部图片
  loadImage('/assets/images/u24.png').then(() => {
    const u24Image = new Rect({
      width: 1860 * 0.75, //调整比例
      height: 49 * 0.75,
      x: (width - 1860 * 0.75) / 2,
      y: height - 49 * 0.75,
      fill: {
        type: 'image',
        url: '/assets/images/u24.png',
        mode: 'cover'
      }
    })
    leafer.tree.add(u24Image)
  })

  // 顶部图片
  loadImage('/assets/images/u348.png').then(() => {
    const u348Image = new Rect({
      width: 1920 * 0.75,
      height: 129 * 0.75,
      x: (width - 1920 * 0.75) / 2,
      y: 0,
      fill: {
        type: 'image',
        url: '/assets/images/u348.png',
        mode: 'cover'
      }
    })
    leafer.tree.add(u348Image)

    // 顶部文字
    const textOnImage = new Text({
      fill: '#F2F3FA',
      fontSize: 32 * 0.75,
      fontFamily: '"微软雅黑 Bold", "微软雅黑", sans-serif',
      fontWeight: 700,
      text: '裁决及效果模拟软件',
      x: (width - (288 * 0.75)) / 2,
      y: 35 * 0.75,
    })
    leafer.tree.add(textOnImage)
  })

  // 左部图片
  loadImage('/assets/images/u23.png').then(() => {
    const u23Image = new Rect({
      width: 43 * 0.75,
      height: 645 * 0.75,
      x: 0,
      y: (height - 645 * 0.75) / 2,
      fill: {
        type: 'image',
        url: '/assets/newImages/u23.png',
        mode: 'cover'
      }
    })
    leafer.tree.add(u23Image)
  })

  // 右部图片
  loadImage('/assets/images/u22.png').then(() => {
    const u22Image = new Rect({
      width: 43 * 0.75,
      height: 645 * 0.75,
      x: width - 43 * 0.75,
      y: (height - 645 * 0.75) / 2,
      fill: {
        type: 'image',
        url: '/assets/newImages/u22.png',
        mode: 'cover'
      }
    })
    leafer.tree.add(u22Image)
  })

  // 动态时间
  const timeText = new Text({
    fill: '#F2F3FA',
    fontSize: 16,
    fontFamily: 'Arial, sans-serif',
    fontWeight: 'normal',
    text: state.currentTime,
    x: 100,
    y: 20,
  })
  leafer.tree.add(timeText)

  // 时间logo
  loadImage('/assets/newImages/u17.png').then((img) => {
    const imageWidth = 50;
    const imageHeight = 50;
    const scaledWidth = imageWidth * 0.75 * 0.5;
    const scaledHeight = imageHeight * 0.75 * 0.5;

    // 创建图片矩形
    const u17Image = new Rect({
      width: scaledWidth,
      height: scaledHeight,
      x: 20,
      y: 20,
      fill: {
        type: 'image',
        url: '/assets/newImages/u17.png',
        mode: 'cover'
      }
    })
    leafer.tree.add(u17Image)

    timeText.x = 20 + scaledWidth + 10
  })

  // 动态更新时间
  setInterval(() => {
    timeText.text = state.currentTime
  }, 1000)

  // 天气logo
  loadImage('/assets/newImages/u21.png').then((img) => {
    const iconWidth = 60;
    const iconHeight = 50;

    const weatherIcon = new Rect({
      width: iconWidth * 0.75 * 0.5,
      height: iconHeight * 0.75 * 0.5,
      x: width - iconWidth - 140,
      y: 20,
      fill: {
        type: 'image',
        url: '/assets/newImages/u21.png',
        mode: 'cover'
      }
    })
    leafer.tree.add(weatherIcon)

    // 天气文本
    const weatherText = new Text({
      fill: '#F2F3FA',
      fontSize: 16,
      fontFamily: 'Arial, sans-serif',
      fontWeight: 'normal',
      text: '32℃',
      x: width - iconWidth - 10 - 100,
      y: 20,
    })
    leafer.tree.add(weatherText)

    // 文字标题背景1
    loadImage('/assets/newImages/u27.png').then(() => {
      const u29Image = new Rect({
        width: 400 * 0.75,
        height: 45 * 0.75,
        x: 105,
        y: 125,
        fill: {
          type: 'image',
          url: '/assets/NewImages/u27.png',
          mode: 'cover'
        }
      })
      leafer.tree.add(u29Image)

      // 文本1
      const u29Text = new Text({
        fill: '#FFFFFF',
        fontFamily: '"微软雅黑 Bold", "微软雅黑", sans-serif',
        fontWeight: 700,
        fontSize: 18 * 0.75,
        text: '裁决模型管理',
        x: 165,
        y: 130,
        textAlign: 'left',
        lineHeight: 20,
      })
      leafer.tree.add(u29Text)

      // 超链接“更多”
      const moreText = new Text({
        fill: '#02FDFF',
        fontFamily: '"微软雅黑", sans-serif',
        // fontWeight: 700,
        fontSize: 15*0.75,
        text: '更多',
        x: 370,
        y: 135,
        textAlign: 'left',
        lineHeight: 15
      })
      leafer.tree.add(moreText)

      // 超链接“更多“的点击事件
      moreText.on('click', () => {
        alert('您点击了“更多”');
      })

      // 文字标题背景2
      const u29ImageClone1 = u29Image.clone()
      u29ImageClone1.x = 105
      u29ImageClone1.y = 280
      leafer.tree.add(u29ImageClone1)

      // 文本2
      const u29TextClone1 = new Text({
        fill: '#FFFFFF',
        fontFamily: '"微软雅黑 Bold", "微软雅黑", sans-serif',
        fontWeight: 700,
        fontSize: 18 * 0.75,
        text: '效果模型管理',
        x: 165,
        y: 285,
        textAlign: 'left',
        lineHeight: 20,
      })
      leafer.tree.add(u29TextClone1)

      //文本标题3
      const u29ImageClone2 = u29Image.clone()
      u29ImageClone2.x = 105
      u29ImageClone2.y = 500
      leafer.tree.add(u29ImageClone2)

      // 文本3
      const u29TextClone2 = new Text({
        fill: '#FFFFFF',
        fontFamily: '"微软雅黑 Bold", "微软雅黑", sans-serif',
        fontWeight: 700,
        fontSize: 18 * 0.75,
        text: '决策规则管束',
        x: 165,
        y: 505,
        textAlign: 'left',
        lineHeight: 20,
      })
      leafer.tree.add(u29TextClone2)

      // 测试滚动表格
      const scrollText = new Text({
        fill: '#FFFFFF',
        fontFamily: '"微软雅黑", "微软雅黑", sans-serif',
        fontWeight: 500,
        fontSize: 16,  // 设置字体大小
        text: `
    01 电子干扰1    电子干扰11   31
    02 电子干扰2    电子干扰22   15
    03 电子干扰3    电子干扰33   21
    04 电子干扰4    电子干扰44   14
    05 电子干扰5    电子干扰55   19
  `,
        x: 165,
        y: 550,
        textAlign: 'left',
        lineHeight: 24,
      })
      leafer.tree.add(scrollText)

      // 滚动效果
      const scrollSpeed = 1; // 控制滚动速度
      let scrollPosition = 550; // 初始滚动位置

      function scrollContent() {
        scrollPosition -= scrollSpeed; // 逐渐向上移动

        // 如果滚动到最底部，则重置位置，实现循环滚动
        if (scrollPosition <= -100) {
          scrollPosition = 550;
        }
        // 更新滚动位置
        scrollText.y = scrollPosition;
        // 继续请求下一帧，保持动画效果
        requestAnimationFrame(scrollContent);
      }

      // 启动滚动效果
      scrollContent();
    })

    // 标题背景上的箭头1
    loadImage('/assets/NewImages/u30.svg').then(() => {
      const u30Image = new Rect({
        width: 39 *0.75,
        height: 40 *0.75,
        x: 140,
        y: 125,
        fill: {
          type: 'image',
          url: '/assets/NewImages/u30.svg',
          mode: 'cover'
        }
      })
      leafer.tree.add(u30Image)

      // 箭头2
      const u30ImageClone1 = u30Image.clone()
      u30ImageClone1.x = 140
      u30ImageClone1.y = 280
      leafer.tree.add(u30ImageClone1)

      //箭头3
      const u30ImageClone2 = u30Image.clone()
      u30ImageClone2.x = 140
      u30ImageClone2.y = 500
      leafer.tree.add(u30ImageClone2)
    })

    // 标题背景4（在右侧）
    loadImage('/assets/newImages/u27.png').then(() => {
      const u29Image = new Rect({
        width: 400 * 0.75,
        height: 45 * 0.75,
        x: 1300,
        y: 125,
        fill: {
          type: 'image',
          url: '/assets/NewImages/u27.png',
          mode: 'cover'
        }
      })
      leafer.tree.add(u29Image)

      // 箭头4
      loadImage('/assets/NewImages/u30.svg').then(() => {
        const u30Image = new Rect({
          width: 39 * 0.75,
          height: 40 * 0.75,
          x: 1335 ,
          y: 125,
          fill: {
            type: 'image',
            url: '/assets/NewImages/u30.svg',
            mode: 'cover'
          }
        })
        leafer.tree.add(u30Image)
      })

      // 文本4
      const u29Text = new Text({
        fill: '#FFFFFF',
        fontFamily: '"微软雅黑 Bold", "微软雅黑", sans-serif',
        fontWeight: 700,
        fontSize: 18 * 0.75,
        text: '裁决模型管理',
        x: 1360,
        y: 130,
        textAlign: 'left',
        lineHeight: 20,
      })
      leafer.tree.add(u29Text)

      // 标题背景5
      const u29ImageClone1 = u29Image.clone()
      u29ImageClone1.x = 1300
      u29ImageClone1.y = 280
      leafer.tree.add(u29ImageClone1)

      // 箭头5
      loadImage('/assets/NewImages/u30.svg').then(() => {
        const u30ImageClone1 = new Rect({
          width: 39 * 0.75,
          height: 40 * 0.75,
          x: 1335,
          y: 280,
          fill: {
            type: 'image',
            url: '/assets/NewImages/u30.svg',
            mode: 'cover'
          }
        })
        leafer.tree.add(u30ImageClone1)
      })

      // 文本5
      const u29TextClone1 = new Text({
        fill: '#FFFFFF',
        fontFamily: '"微软雅黑 Bold", "微软雅黑", sans-serif',
        fontWeight: 700,
        fontSize: 18 * 0.75,
        text: '效果模型管理',
        x: 1360,
        y: 285,
        textAlign: 'left',
        lineHeight: 20,
      })
      leafer.tree.add(u29TextClone1)

      // 标题背景6
      const u29ImageClone2 = u29Image.clone()
      u29ImageClone2.x = 1300
      u29ImageClone2.y = 500
      leafer.tree.add(u29ImageClone2)

      // 箭头6
      loadImage('/assets/NewImages/u30.svg').then(() => {
        const u30ImageClone2 = new Rect({
          width: 39 * 0.75,
          height: 40 * 0.75,
          x: 1335,
          y: 500,
          fill: {
            type: 'image',
            url: '/assets/NewImages/u30.svg',
            mode: 'cover'
          }
        })
        leafer.tree.add(u30ImageClone2)
      })

      // 文本6
      const u29TextClone2 = new Text({
        fill: '#FFFFFF',
        fontFamily: '"微软雅黑 Bold", "微软雅黑", sans-serif',
        fontWeight: 700,
        fontSize: 18 * 0.75,
        text: '决策规则管束',
        x: 1360,
        y: 505,
        textAlign: 'left',
        lineHeight: 20,
      })
      leafer.tree.add(u29TextClone2)

    })
  })
})

// 加载图片并返回其实际尺寸
function loadImage(url: string): Promise<HTMLImageElement> {
  return new Promise((resolve, reject) => {
    const img = new Image()
    img.src = url
    img.onload = () => resolve(img)
    img.onerror = (err) => reject(err)
  })
}

// 创建文本的函数
const createText = (text: string): Text => {
  return new Text({
    fill: '#888',
    fontSize: 20,
    fontFamily: 'Inter, system-ui, Avenir, Helvetica, Arial, sans-serif',
    text
  })
}
</script>

<template>
  <div id="leafer-view"></div>
</template>

<style scoped>
#leafer-view {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
