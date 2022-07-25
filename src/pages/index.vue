<script setup lang="ts">
const allIdeals = [
  {
    name: 'Slider',
    path: 'slider',
    desc: '多种方式实现轮播图',
    icon: 'soil-moisture-global',
  },
  {
    name: 'Drag',
    path: 'drag',
    desc: '鼠标拖动',
    icon: 'move',
  },
  {
    name: 'FiveStars',
    path: 'five',
    desc: '五子棋游戏',
    icon: 'gateway',
  },
]
</script>

<template>
  <h1 text-size-8 w-200 mx-auto text-left mb-7>
    一些小玩意儿
  </h1>
  <div grid="~ cols-2 gap-2" w-200 mx-auto>
    <div v-for="item in allIdeals" :key="item.path" b-rounded>
      <router-link :to="item.path">
        <div flex dark:hover="bg-stone-9" light:hover="bg-gray-400" p-2>
          <div i-carbon-dicom-overlay h-auto text-size-10 />
          <div ml-3 flex-1 text-left>
            <div text-size-5>
              {{ item.name }}
            </div>
            <div text-size-2 color-blueGray>
              {{ item.desc }}
            </div>
          </div>
        </div>
      </router-link>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
