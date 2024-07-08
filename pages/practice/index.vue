<script setup>
  const morseDict = [
    { letter: 'A', morse: '.-', type: 'letter' },
    { letter: 'B', morse: '-...', type: 'letter' },
    { letter: 'C', morse: '-.-.', type: 'letter' },
    { letter: 'D', morse: '-..', type: 'letter' },
    { letter: 'E', morse: '.', type: 'letter' },
    { letter: 'F', morse: '..-.', type: 'letter' },
    { letter: 'G', morse: '--.', type: 'letter' },
    { letter: 'H', morse: '....', type: 'letter' },
    { letter: 'I', morse: '..', type: 'letter' },
    { letter: 'J', morse: '.---', type: 'letter' },
    { letter: 'K', morse: '-.-', type: 'letter' },
    { letter: 'L', morse: '.-..', type: 'letter' },
    { letter: 'M', morse: '--', type: 'letter' },
    { letter: 'N', morse: '-.', type: 'letter' },
    { letter: 'O', morse: '---', type: 'letter' },
    { letter: 'P', morse: '.--.', type: 'letter' },
    { letter: 'Q', morse: '--.-', type: 'letter' },
    { letter: 'R', morse: '.-.', type: 'letter' },
    { letter: 'S', morse: '...', type: 'letter' },
    { letter: 'T', morse: '-', type: 'letter' },
    { letter: 'U', morse: '..-', type: 'letter' },
    { letter: 'V', morse: '...-', type: 'letter' },
    { letter: 'W', morse: '.--', type: 'letter' },
    { letter: 'X', morse: '-..-', type: 'letter' },
    { letter: 'Y', morse: '-.--', type: 'letter' },
    { letter: 'Z', morse: '--..', type: 'letter' },
    { letter: '0', morse: '-----', type: 'number' },
    { letter: '1', morse: '.----', type: 'number' },
    { letter: '2', morse: '..---', type: 'number' },
    { letter: '3', morse: '...--', type: 'number' },
    { letter: '4', morse: '....-', type: 'number' },
    { letter: '5', morse: '.....', type: 'number' },
    { letter: '6', morse: '-....', type: 'number' },
    { letter: '7', morse: '--...', type: 'number' },
    { letter: '8', morse: '---..', type: 'number' },
    { letter: '9', morse: '----.', type: 'number' }
  ];

  const questionMode = ref('letter')
  const allowNumbers = ref(false)
  const givenAnswer = ref("")
  const currentQType = ref("")
  const feedbackText = ref("")
  const showingHelpModal = ref(false)
  
  const currentQuestion = ref({
    letter: 'A',
    morse: '.-',
    type:''
  })

  const getNewQuestion = () => {
    const chosenQ = morseDict[Math.floor(Math.random() * morseDict.length)]
    if(allowNumbers.value) {
      currentQuestion.value = chosenQ
    } else {
      if(chosenQ.type === 'letter') {
        currentQuestion.value = chosenQ
      } else {
        getNewQuestion()
      }
    }
  }

  const getCardText = () => {
    if(questionMode.value === 'morse') {
      currentQType.value = 'morse'
      return currentQuestion.value.morse
    }
    if(questionMode.value === 'letter') {
      currentQType.value = 'letter'
      return currentQuestion.value.letter
    }
    if(Math.random() > 0.5) {
      currentQType.value = 'morse'
      return currentQuestion.value.morse
    } else {
      currentQType.value = 'letter'
      return currentQuestion.value.letter
    }
  }

  const handleSubmitClick = () => {
    if(checkAnswer()) {
      feedbackText.value = "Correct!"
      getNewQuestion()
    } else {
      feedbackText.value = "Try again..."
    }
  }

  const checkAnswer = () => {
    if(currentQType.value === 'letter') {
      return givenAnswer.value == currentQuestion.value.morse
    } else {
      return givenAnswer.value.toLowerCase() == currentQuestion.value.letter.toLowerCase()
    }
  }
</script>

<template>
  <div>
    <div class="absolute top-0 left-0 w-screen p-2">
      <fieldset class="text-sm flex gap-2 justify-center justify" @change="getNewQuestion">
        <input type="radio" id="letter" value="letter" name="mode" v-model="questionMode"/>
        <label for="letter">Show Character</label>
        <input type="radio" id="morse" value="morse" name="mode" v-model="questionMode"/>
        <label for="morse">Show Morse</label>
        <input type="radio" id="both" value="both" name="mode" v-model="questionMode"/>
        <label for="both">Show Both</label>
      </fieldset>

      <label for="allow-numbers">Allow Numbers?: </label>
      <input id="allow-numbers" type="checkbox" v-model="allowNumbers"/>
    </div>

    <div class="flex flex-col items-center justify-center">
      <div class="w-48 h-48 text-9xl flex items-center justify-center">
        {{ getCardText() }}
      </div>
      <div>
        <form @submit.prevent="handleSubmitClick" class="flex items-center gap-2">
          <input type="text" class="border border-black text-black rounded-md pl-1" v-model="givenAnswer" autofocus />
          <input type="submit" value="Submit" class="bg-slate-200 border border-black px-2 rounded-md" />
        </form>
      </div>

      <span>{{ feedbackText }}</span>

      <Back class="mt-4"/>
    </div>

    <button class="z-50 absolute right-4 bottom-4 rounded-full bg-white border-4 border-black text-2xl font-bold w-12 h-12 flex items-center justify-center" @click="showingHelpModal = !showingHelpModal">
      ?
    </button>
    <div v-if="showingHelpModal" class="absolute top-0 left-0 w-screen h-screen z-40 bg-slate-400 bg-opacity-70 flex flex-col justify-center items-center">
      <LetterGrid />
    </div>
  </div>
</template>

<style scoped>
  
</style>