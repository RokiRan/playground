<script lang='ts' setup>
const prop = defineProps(['src'])
</script>

<template>
  <img :src="prop.src" class="w-100%" object-cover="" block="" w-full="" h-full="" bg-gray-400:20="" b-rd-3>
</template>
