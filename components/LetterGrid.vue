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

</script>

<template>
  <div class="flex flex-col items-center gap-4">
    <div class="grid grid-cols-5 gap-4">
      <LetterCell v-for="l in morseDict" :letter="l.letter" :morse="l.morse"/>
    </div>
  </div>
</template>