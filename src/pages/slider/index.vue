<script setup lang="ts">
const imgs = ['https://cdn.pixabay.com/photo/2015/01/07/15/51/woman-591576_960_720.jpg', 'https://cdn.pixabay.com/photo/2014/07/31/22/50/photographer-407068_960_720.jpg', 'https://cdn.pixabay.com/photo/2020/02/02/14/03/cat-4813099_960_720.jpg']
const slider = ref<HTMLDivElement>()
const isStartDrop = ref(false)
const startPoint = reactive({ x: 0, y: 0 })
onMounted(() => {
  // window.setInterval(() => {
  //   slider.value.scrollBy(offsetX++, 0)
  //   console.log(slider.value.scrollWidth, offsetX)
  //   if (slider.value.scrollWidth <= offsetX * 20)
  //     offsetX = 0
  // }, 1000)
})
const moveForward = () => {
  // slider.value.offsetX = 100
  slider.value!.scrollBy(400, 0)
}
const moveBack = () => {
  // slider.value.offsetX = 100
  slider.value!.scrollBy(-400, 0)
}
const onDrag = (e: MouseEvent) => {
  // slider.value
  // const deltaLeft = e.clientX - e.target!.offsetLeft
  // const deltaTop = e.clientY - e.target!.offsetTop
  if (!isStartDrop.value)
    return
  slider.value!.scrollBy(e.offsetX - startPoint.x, 0)
}
const onMouseDown = (e: MouseEvent) => {
  isStartDrop.value = true
  startPoint.x = e.offsetX
}
const onMouseUp = (e: MouseEvent) => {
  isStartDrop.value = false
  isStartDrop.value = false
  startPoint.x = 0
}
</script>

<template>
  <div>
    <div pos="relative" w-100 mx-auto>
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
    </div>
  </div>
</template>
