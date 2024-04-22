<script setup lang="ts">
import Card from './CardItem.vue'
import { ref,  onMounted } from 'vue'
import Swal from 'sweetalert2'

interface PROPS {
  cardsContext: Array<any>
}

interface EMITS {
  (e:string):void
}

const windowHeight =window.innerWidth<=800 ? 550 :window.innerHeight


const emit = defineEmits<EMITS>()
const arr = ref<any>([])
const props = defineProps<PROPS>()

const handleCheck = (e:any) => {
  arr.value.push(e)

  if (arr.value.length === 2 && arr.value[0].value === arr.value[1].value) {
    handleClearArr()
    const disabledElements = document.querySelectorAll('.disabled')
    if (disabledElements && disabledElements.length === props.cardsContext.length - 1) {
      setTimeout(() => emit('onOpenResult'), 1000)
    }
  } else if (arr.value.length === 2 && arr.value[0].value !== arr.value[1].value) {
    setTimeout(() => {
      arr.value[0].flipStatus = false
      arr.value[1].flipStatus = false
    }, 500)
  }
}

const handleClearArr = () => {
  arr.value = []
}

onMounted(() => {
  Swal.fire({
    title: 'Some Advise👌',
    text: "Because it's a  demo version, please play slowly!",
    icon: 'info'
  })

})
</script>

<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 + 16) *
          Math.sqrt(cardsContext.length)
        }px`
      }"
    >
      <card
        v-for="(card, index) in props.cardsContext"
        :key="index"
        :imgUrl="`images/${card}.png`"
        :card="{ index, card, arr }"
        :cardsContext="props.cardsContext"
        @onFlip="handleCheck($event)"
        @onClearArr="handleClearArr()"
      />
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
}

.screen__inner {
  width: calc(424px);
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}

@media screen and (max-width: 500px) {
  .screen {
    overflow: hidden;
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    display: flex;
    justify-content: center;

    background-color: var(--dark);
    color: var(--light);
  }

  .screen__inner {
    width: 50%;
    display: flex;
    flex-wrap: wrap;
    margin: 2rem auto;
    justify-content: center;
    align-content: center;
  }
}
</style>
