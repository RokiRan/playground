<script setup lang="ts">
const Audio = ref<HTMLAudioElement>()
const Video = ref<HTMLVideoElement>()
onMounted(() => {
  nextTick(() => {
    // eslint-disable-next-line no-console
    console.log('开始播放')
    Video.value!.play()
    Audio.value!.play()
  })
})
</script>

<template>
  <div mt-5>
    <audio ref="Audio" mx-auto src="/audio/孙伯纶 - 如果你也听说 (选择导师：那英).mp3" w-90vw h-12 controls />
  </div>
  <div mt-5>
    <video ref="Video" mx-auto src="/video/yourName.mp4" w-90vw controls autoplay />
  </div>
</template>

<style scoped>

</style>
