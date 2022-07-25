<script lang='ts' setup>
</script>

<template>
  <div>
    <div w-100 h-100 mx-auto display="inline-block'" flex="~ wrap">
      <div v-for="box in 400" :key="box" inline-block w-5 h-5 :style="{ background: `rgba(${1 + box},${255 - box},${10 + box * 0.8},0.5)` }" />
    </div>
  </div>
</template>
