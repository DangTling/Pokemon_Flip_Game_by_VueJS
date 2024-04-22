<script setup lang="ts">
import { ref } from 'vue'
import './assets/styles/global.css'
import { shuffled } from '@/utils'
import MainScreen from './components/MainScreen.vue'
import CopyRight from '@/components/CopyRight.vue'
import InteractScreen from '@/components/InteractScreen.vue'
import ResultScreen from '@/components/ResultScreen.vue'

const status = ref('default')
const cardsContext = ref<number[]>([])
const totalBlock = ref(0)
const startedAt = ref<number>(0)
const timer = ref(0)
const handleChangeScreen = (e:any) => {
  console.log('Game is starting ...!')
  totalBlock.value = e.totalBlock
  const arr1 = Array.from({ length: totalBlock.value / 2 }, (_, i) => i + 1)
  const arr2 = [...arr1]
  const arr = [...arr1, ...arr2]
  cardsContext.value = shuffled(shuffled(shuffled(shuffled(arr))))
  startedAt.value = new Date().getTime()
  status.value = 'inMatch'
}

const handleResult = () => {
  console.log('This is result screen!')
  timer.value = new Date().getTime() - startedAt.value
  status.value = 'result'
}

const handleStartAgain = () => {
  status.value = 'default'
}
</script>

<template>
  <main-screen v-if="status === 'default'" @onStart="handleChangeScreen($event)" />
  <InteractScreen
    v-else-if="status === 'inMatch'"
    :cardsContext="cardsContext"
    @onOpenResult="handleResult"
  />
  <ResultScreen v-else :timer="timer" @startAgain="handleStartAgain" />
  <CopyRight/>
</template>
