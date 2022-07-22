<script lang='ts' setup>
const target = ref<HTMLImageElement>()
const box = ref<HTMLImageElement>()
const offsetTop = ref(0)
const offsetLeft = ref(0)
const isStartDrop = ref(false)

const startPoint = reactive({
  x: 0,
  y: 0,
})
const mousePoint = reactive({ // 鼠标实时坐标
  x: 0,
  y: 0,
})
const mouseInScreen = reactive({ x: 0, y: 0 })
const targetPoint = reactive({ x: 0, y: 0 })
const boxPosition = reactive({ x: 0, y: 0 })
const boxContainer = { width: 0, height: 0 } // box 容器大小
onMounted(() => {
  // x.value = target.value?.style.left || ''
  // y.value = target.value?.style.top || ''
  offsetTop.value = target.value?.offsetTop || 0
  offsetLeft.value = target.value?.offsetLeft || 0
  boxPosition.x = box.value!.offsetTop
  boxPosition.y = box.value!.offsetLeft
  boxContainer.height = box.value!.offsetHeight
  boxContainer.width = box.value!.offsetWidth
})
const onMouseDown = (e: MouseEvent) => {
  if (e.target !== target.value || isStartDrop.value)
    return
  startPoint.x = e.offsetX
  startPoint.y = e.offsetY
  isStartDrop.value = true // 标记可以拖动
}
const onMouseUp = (e: MouseEvent) => {
  isStartDrop.value = false
}
const onMove = (e: MouseEvent) => {
  e.stopPropagation()
  e.preventDefault()
  mousePoint.x = e.offsetX
  mousePoint.y = e.offsetY
  // console.log(e)
  mouseInScreen.x = e.clientX // 屏幕坐标
  mouseInScreen.y = e.clientY
  if (!isStartDrop.value)
    return
  let top = (mouseInScreen.y - boxPosition.x) - startPoint.y // 实际坐标 = 鼠标屏幕坐标 - 容器上左偏移 - 目标内鼠标坐标偏移
  let left = (mouseInScreen.x - boxPosition.y) - startPoint.x
  // 判断边界
  if (top < 0)
    top = 0
  if (top > boxContainer.height - target.value!.offsetHeight)
    top = boxContainer.height - target.value!.offsetHeight - 2
  if (left < 0)
    left = 0
  if (left > boxContainer.width - target.value!.offsetWidth)
    left = boxContainer.width - target.value!.offsetWidth - 2
  target.value!.style.top = `${top}px`
  target.value!.style.left = `${left}px`
}
</script>

<template>
  <div ref="box" w-100 h-100 border-1 mx-auto pos="relative" @mousemove="onMove" @mouseup="onMouseUp">
    <div ref="target" w-20 h-20 border-1 inline-block top-20 left-20 pos="absolute" cursor="hover:move" @mousedown="onMouseDown" />
  </div>
  <div>
    <span>boxPosition: {{ boxPosition.x }} , {{ boxPosition.y }}</span> <br>
    <span>startPoint: {{ startPoint.x }} , {{ startPoint.y }}</span> <br>
    <span>offsetTop: {{ offsetTop }}</span> <br>
    <span>offsetLeft: {{ offsetLeft }}</span><br>
    <!-- <span>movementX: {{ mx }}</span><br> -->
    <span>mousePoint: {{ mousePoint.x }} , {{ mousePoint.y }}</span><br>
    <span>targetPoint: {{ targetPoint.x }} , {{ targetPoint.y }}</span><br>
    <span>mouseInScreen: {{ mouseInScreen.x }} , {{ mouseInScreen.y }}</span><br>
  </div>
</template>
