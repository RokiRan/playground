<script lang="ts" setup>
import MyInputVue from '~/components/MyInput.vue'
const initValue = ref('this is base info')
</script>

<template>
  <div>
    <MyInputVue v-modal:value="initValue" />
  </div>
</template>

<style scoped lang='less'>

</style>
