<template>
  <div class="screen">
    <h1>Pokemon Match</h1>
    <h3>Select mode to start game</h3>
    <div class="modes">
      <button @click="handleStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="handleStart(36)">
        <span>6x6</span>
        <span>Medium</span>
      </button>
      <button @click="handleStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="handleStart(256)">
        <span>16x16</span>
        <span>Hell</span>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">


interface PROPS {
  (e:string,value:object):void
}

const  emit  = defineEmits<PROPS>()
const handleStart = (totalBlock:number) => {
  emit('onStart', { totalBlock })
}
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: var(--dark);
  color: var(--light);
}


.screen h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
}

.screen p {
  font-size: 2rem;
}

.modes {
  display: flex;
  margin-top: 2rem;
}

.modes button {
  font: var(--font);
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

.modes button:hover {
  background-color: var(--light);
  color: var(--dark);
}

.modes button span:first-child {
  font-size: 2rem;
}

.modes button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
}

@media screen and (max-width: 500px) {
  .screen {
    overflow: hidden;
    width: 100vw;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: var(--dark);
    color: var(--light);
    text-align: center;
  }
  .screen h1 {
    font-size: 3rem;
    text-transform: uppercase;
    margin: 0 auto;
  }
  .modes  button {
    font: var(--font);
    width: 80px;
    height: 80px;
    margin: 0 5px;
    border: 1px solid var(--light);
    color: var(--light);
    display: flex;
    flex-direction: column;
    border-radius: 1rem;
    align-items: center;
    justify-content: center;
    transition: background 0.3s ease-in-out;
  }
}

</style>
