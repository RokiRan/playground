<script lang='ts' setup>
const target = ref<HTMLImageElement>()
const x = ref('')
const y = ref('')
const offsetTop = ref(0)
const offsetLfet = ref(0)
const isStartDrop = ref(false)
const startPoint = reactive({
  x: 0,
  y: 0,
})
onMounted(() => {
  x.value = target.value?.style.left || ''
  y.value = target.value?.style.top || ''
  offsetTop.value = target.value?.offsetTop || 0
  offsetLfet.value = target.value?.offsetLeft || 0
})
const onMouseDown = (e: MouseEvent) => {
  startPoint.x = e.offsetX
  startPoint.y = e.offsetY
  isStartDrop.value = true // 标记可以拖动
}
const onMouseUp = (e: MouseEvent) => {
  isStartDrop.value = false
}
const onDrag = (e: MouseEvent) => {
  if (!isStartDrop.value)
    return
  const x = e.offsetX
  const y = e.offsetY
  const offsetPoint = {
    x: x - startPoint.x,
    y: y - startPoint.y,
  }
  // eslint-disable-next-line no-console
  console.log(offsetPoint)
//   target.value!.style.top = `${offsetPoint.x}px`
//   target.value!.style.left = `${offsetPoint.y}px`
}
</script>

<template>
  <div w-100 h-100 border-1 mx-auto pos="relative">
    <div ref="target" w-20 h-20 border-1 inline-block pos="absolute" cursor="hover:move" @mousemove="onDrag" @mousedown="onMouseDown" @mouseup="onMouseUp" />
  </div>
  <div>
    <span>offsetTop:{{ offsetTop }}</span> <br>
    <span>offsetLfet:{{ offsetLfet }}</span>
  </div>
</template>
