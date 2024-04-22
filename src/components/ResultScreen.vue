<script setup lang="ts">
import { toRefs } from 'vue'

interface EMIT{
  (e:string):void
}
interface PROPS {
  timer:number
}
const props = defineProps<PROPS>()
const {timer} = toRefs(props)
const emit = defineEmits<EMIT>()
const handleStartAgain = () => {
  emit('startAgain')
}
</script>

<template>
  <div class="screen">
    <h1>✨ Congratulation ✨</h1>
    <p>{{ Math.round(timer / 1000) }} Seconds</p>
    <button @click="handleStartAgain">Start Again</button>
    <br />
    <br />
    <div >
      <h5>Connect with me</h5>
      <p>
        <a href="https://github.com/DangTling">
          <img src="https://img.icons8.com/fluent/48/000000/github.png" alt=""/>
        </a>
        <a href="https://www.instagram.com/dvtlinh26/">
          <img src="https://img.icons8.com/fluent/48/000000/instagram-new.png"  alt=""/>
        </a>
        <a href="mailto:dvtlinh26@gmail.com">
          <img
            src="https://img.icons8.com/fluency/48/000000/gmail-new.png"  alt=""/>
        </a>
      </p>
    </div>
  </div>
</template>



<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.screen h1 {
  font-size: 5rem;
}

.screen h3 {
  margin-top: 1.5rem;
  font-size: 3rem;
}

.screen button {
  font: var(--font);
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  margin: 1rem;
  padding: 1rem 1.25rem;
  border-radius: 0.5rem;
  font-size: 1.25rem;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

.screen button:hover {
  background-color: var(--light);
  color: var(--dark);
}
</style>
