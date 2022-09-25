<script lang="ts" setup>
const emit = defineEmits(['value:update'])
const value = ref('123')
</script>

<template>
  <div>
    <input :value="value" type="text">
  </div>
</template>

<style scoped lang='less'>

</style>
