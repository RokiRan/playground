<script lang='ts' setup>
import { Starport } from 'vue-starport'
import { useRouter } from 'vue-router'
const router = useRouter()
</script>

<template>
  <div>
    <div mt-30 overflow="hidden" @click="router.back()">
      <Starport port="user2" style="height:600px;">
        <Image src="https://cdn.pixabay.com/photo/2022/07/18/19/57/dog-7330712_960_720.jpg" style="filter: blur(.5rem);" />
      </Starport>
    </div>
  </div>
</template>

<style>
/* [data-starport-craft] {
  background: rgba(130, 238, 130, 0.333);
}
[data-starport-proxy]:not([data-starport-landed]) {
  background: rgba(224, 216, 216, 0.333);
} */
</style>
