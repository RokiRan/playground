<script setup lang="ts">
const Audio = ref<HTMLAudioElement>()
const Video = ref<HTMLVideoElement>()
const AudioBtn = ref<HTMLDivElement>()
const VideoBtn = ref<HTMLDivElement>()
onMounted(() => {
  Audio.value!.play()
  Video.value!.play()
})
document.addEventListener('WeixinJSBridgeReady', () => {
  // eslint-disable-next-line no-console
  console.log('WeixinJSBridgeReady')
  Audio.value!.play()
  Video.value!.play()
}, false)
</script>

<template>
  <div mt-5>
    <audio ref="Audio" mx-auto src="/audio/孙伯纶 - 如果你也听说 (选择导师：那英).mp3" w-90vw h-12 controls autoplay />
  </div>
  <div mt-5>
    <video ref="Video" mx-auto src="/video/yourName.mp4" w-90vw controls autoplay />
  </div>
  <div>
    <div ref="AudioBtn" class="btn" @click="Video?.play()">
      播放视频
    </div>
    <div ref="VideoBtn" ml-5 mt-5 class="btn" @click="Audio?.play()">
      播放音频
    </div>
  </div>
</template>

<style scoped>

</style>
