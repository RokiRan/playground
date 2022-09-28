<script setup lang="ts">
const imgs: any[] = ['https://cdn.pixabay.com/photo/2021/09/14/10/36/sea-lion-6623606_960_720.jpg', 'https://cdn.pixabay.com/photo/2022/09/19/09/27/nuts-7465088_960_720.jpg', 'https://cdn.pixabay.com/photo/2015/01/07/15/51/woman-591576_960_720.jpg', 'https://cdn.pixabay.com/photo/2014/07/31/22/50/photographer-407068_960_720.jpg', 'https://cdn.pixabay.com/photo/2020/02/02/14/03/cat-4813099_960_720.jpg']
imgs.forEach((img, index) => {
  imgs[index] = {
    img,
    index,
  }
})
imgs.unshift(imgs[imgs.length - 1])
imgs.push(imgs[1])

const slider2 = ref<HTMLDivElement>()
const isStartDrop = ref(false)
const startPoint = reactive({ x: 0 })
const currentIndex = ref(1)
const totalItem = ref(imgs.length)
const offsetX = ref(0)
const width = ref(0)
const originPoint = ref(0) // 每次移动后的偏移量
const moveX = ref(0) // 每次move的偏移
const animateTime = 800
const allowMove = ref(true)
onMounted(() => {
  width.value = slider2.value?.clientWidth || 0
  offsetX.value = -width.value
  isStartDrop.value = true
})
const moveForward = () => {
  if (!allowMove.value)
    return
  if (currentIndex.value < totalItem.value - 1)
    currentIndex.value += 1
  else currentIndex.value = 0
  offsetX.value = 0 - width.value * currentIndex.value
  originPoint.value = unref(offsetX.value)
  allowMove.value = false
  moveDone()
}
const moveBack = () => {
  if (!allowMove.value)
    return
  if (currentIndex.value > 0)
    currentIndex.value -= 1
  else currentIndex.value = totalItem.value - 1
  offsetX.value = 0 - width.value * currentIndex.value
  originPoint.value = unref(offsetX.value)
  allowMove.value = false
  moveDone()
}

const onDrag = (e: TouchEvent) => {
  if (!isStartDrop.value || !allowMove.value)
    return
  const deltaLeft = e.touches[0].pageX - startPoint.x

  // console.log('clientX', deltaLeft)
  moveX.value = deltaLeft
  let dis = deltaLeft
  if (Math.abs(deltaLeft) > width.value) {
    // 拖动的距离超过了单个宽度
    dis = width.value * (deltaLeft < 0 ? -1 : 1)
  }
  offsetX.value = dis + originPoint.value
}
const onMouseDown = (e: TouchEvent) => {
  if (!allowMove.value)
    return
  isStartDrop.value = true
  startPoint.x = e.touches[0].pageX
}
const onMouseUp = (e: TouchEvent) => {
  if (!allowMove.value)
    return
  isStartDrop.value = false
  offsetX.value = unref(originPoint.value)
  originPoint.value = unref(offsetX.value)
  // const _OffsetX = unref(originPoint.value)
  if (Math.abs(moveX.value) > width.value / 3)
    moveX.value < 0 ? moveForward() : moveBack()

  moveX.value = 0
  // currentIndex.value = Math.abs(offsetX.value / width.value)
  // startPoint.x = e.touches[0].pageX
}
function moveDone() {
  setTimeout(() => {
    isStartDrop.value = true
    const curr = Math.abs(offsetX.value / width.value)
    if (curr === 0) {
      currentIndex.value = totalItem.value - 2
      offsetX.value = -width.value * currentIndex.value
      console.log('要平移到倒数第二张了', offsetX.value)
    }
    else if (curr === (totalItem.value - 1)) {
      currentIndex.value = 1
      offsetX.value = -width.value
      console.log('平移到正数第二张', offsetX.value)
    }

    // isStartDrop.value = false
    allowMove.value = true
  }, animateTime + 50)
}
</script>

<template>
  <div @touchmove="onDrag" @touchstart="onMouseDown" @touchend="onMouseUp">
    <!-- <div pos="relative" w-100 mx-auto>
      <div
        i-carbon-chevron-left
        inline-block pos="absolute top-31 left-0"
        cursor="pointer"
        @click="moveBack"
      />
      <div
        i-carbon-chevron-right
        inline-block pos="absolute top-31 right-1"
        cursor="pointer"
        @click="moveForward"
      />
      <div ref="slider" flex="~ row" w-100 overflow="hidden" mx-auto @mousemove="onDrag" @mousedown="onMouseDown" @mouseup="onMouseUp">
        <img v-for="img in imgs" :key="img" :src="img" w-100>
      </div>
    </div> -->
    <div pos="relative" w-100 mx-auto>
      <div ref="slider2" w-100 class="relative" flex="~" overflow="hidden">
        <div v-for="img in imgs" :key="img.index" class="relative w-100% flex-shrink-0 h-60" :class="isStartDrop ? '' : 'transition-during'" :style="{ transform: `translate3d(${offsetX}px, 0px, 0px)` }" @dragstart.prevent.stop>
          <img :src="img.img" class=" w-100 h-100%">
          <div class="absolute bottom-0 bg-dark-200 w-100% " style="background: rgba(0,0,0,0.4)">
            {{ img.index + 1 }}
          </div>
        </div>
      </div>
      <div
        i-carbon-chevron-left
        inline-block pos="absolute top-26 left-0"
        cursor="pointer"
        @click.self.stop="moveBack"
      />
      <div
        i-carbon-chevron-right
        inline-block pos="absolute top-26 right-1"
        cursor="pointer"
        @click.self.stop="moveForward"
      />
    </div>
    <div>{{ currentIndex }}</div>
  </div>
</template>

<style>
  .transition-during {
    transition-duration: 800ms;
  }
</style>
