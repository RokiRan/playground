<script lang='ts' setup>
import { useRouter } from 'vue-router'
import { Starport } from 'vue-starport'

const router = useRouter()
const goSecond = (path: string) => {
  router.push(path)
}
interface Link {
  id: string
  path: string
  img: string
}
const linkArr = reactive<Link[]>([
  {
    id: 'user1',
    path: '/starport/second',
    img: 'https://cdn.pixabay.com/photo/2014/10/27/19/18/baby-shoes-505471_960_720.jpg',
  },
  {
    id: 'user2',
    path: '/starport/third',
    img: 'https://cdn.pixabay.com/photo/2022/07/25/15/18/cat-7344042_960_720.jpg',
  },
  {
    id: 'user3',
    path: '/starport/fourth',
    img: 'https://cdn.pixabay.com/photo/2022/07/18/19/57/dog-7330712_960_720.jpg',
  },
])
</script>

<template>
  <div>Hi</div>
  <div>
    <Starport v-for="item in linkArr" :key="item.id" :port="item.id" object-cover h-20 mt-5 @click="goSecond(item.path)">
      <Image :src="item.img" />
    </Starport>
  </div>
</template>
