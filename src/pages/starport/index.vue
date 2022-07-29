<script lang='ts' setup>
import { useRouter } from 'vue-router'
import { Starport } from 'vue-starport'

const router = useRouter()
const goSecond = () => {
  router.push('/starport/second')
}
</script>

<template>
  <div>Hi</div>
  <div>
    <Starport port="starImg" object-cover h-20 @click="goSecond">
      <Image src="https://cdn.pixabay.com/photo/2014/10/27/19/18/baby-shoes-505471_960_720.jpg" />
    </Starport>
  </div>
</template>
