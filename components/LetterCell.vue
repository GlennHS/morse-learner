<script setup>
  const props = defineProps({
    letter: String,
    morse: String
  })
  const showingModal = ref(false)

  const handleCellClick = () => {
    showingModal.value = true
    const audioUrl = `/audio/${props.letter.toLowerCase()}.mp3`
    const audio = new Audio(audioUrl);
    audio.volume = 0.4
    audio.play();
  }
</script>

<template>
  <div>
    <div v-if="!showingModal" class="p-1 w-12 h-12 font-bold bg-white border border-black flex flex-col justify-center items-center" @click="handleCellClick">
      <span class="text-lg">{{ letter }}</span>
      <span class="text-sm leading-3">{{ morse }}</span>
    </div>

    <div v-if="showingModal" class="absolute top-0 left-0 w-screen h-screen z-50 bg-slate-400 bg-opacity-70 flex flex-col justify-center items-center" @click="showingModal = false">
      <div class="flex flex-col justify-evenly items-center border-2 border-black bg-white aspect-square p-8">
        <span class="text-5xl">{{ letter }}</span>
        <span class="text-2xl">{{ morse }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
  
</style>