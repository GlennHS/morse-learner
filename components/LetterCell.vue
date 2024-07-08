<script setup>
  const props = defineProps({
    letter: String,
    morse: String
  })
  const showingModal = ref(false)
</script>

<template>
  <div>
    <div v-if="!showingModal" class="p-1 w-10 h-10 text-2xl font-bold bg-white border border-black flex justify-center items-center" @click="showingModal = true">
      {{ letter }}
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