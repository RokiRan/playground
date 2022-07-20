<script setup lang="ts">
const allIdeals = [
  {
    name: 'Slider',
    path: 'slider',
  },
  {
    name: 'Slider',
    path: 'ideal',
  },
  {
    name: 'Slider',
    path: 'ideal',
  },
  {
    name: 'Slider',
    path: 'ideal',
  },
  {
    name: 'Slider',
    path: 'ideal',
  },
]
</script>

<template>
  <div grid="~ cols-3 gap-2">
    <div v-for="item in allIdeals" :key="item.path" border="~ border-1" b-rounded h-30>
      <router-link :to="item.path" text-size-10>
        {{ item.name }}
      </router-link>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
