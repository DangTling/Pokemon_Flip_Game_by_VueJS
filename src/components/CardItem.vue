<script lang="ts" setup >
import { ref, watchEffect } from 'vue'

interface PROPS {
  imgUrl: String,
  card: {
    index: number,
    card: number,
    arr: Array<any>
  },
  cardsContext: Array<any>
}

interface EMITS {
  (e:string, value?:any):void
}

const isFlipped = ref(false)
const emit = defineEmits<EMITS>()
const windowHeight =window.innerWidth<=500 ? 600 :window.innerHeight


const props = defineProps<PROPS>()

const handleFlip = () => {
  if (props.card.arr.length < 2) {
    isFlipped.value = !isFlipped.value
    const data_up = {
      index: props.card.index,
      value: props.card.card,
      flipStatus: isFlipped.value
    }
    emit('onFlip', data_up)
  }
}
watchEffect(() => {
  if (
    (props.card.arr.length === 2 && props.card.arr[0].index === props.card.index) ||
    (props.card.arr.length === 2 && props.card.arr[1].index === props.card.index)
  ) {
    isFlipped.value = props.card.arr[0].flipStatus
    setTimeout(() => {
      emit('onClearArr')
    }, 600)
  }
})
</script>

<template>
  <div
    class="card"
    :class="{ disabled: isFlipped }"
    @click="handleFlip"
    :style="{
      height: `${(windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
      width: `${(((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4}px`,
      perspective: `${((((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4) * 2}px`
    }"
  >
    <div class="card_inner" :class="{ is_flipped: isFlipped }">
      <div class="card_face card_front">
        <div
          class="card_content"
          :style="{
            'background-size': `${
              (((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 / 3
            }px ${(((windowHeight - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 / 3}px`
          }"
        ></div>
      </div>
      <div class="card_face card_back">
        <div
          class="card_content"
          :style="{ backgroundImage: `url(${'/src/assets/' + props.imgUrl})` }"
        ></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}
.card.disabled {
  pointer-events: none;
  opacity: 0.9;
}
.card_inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.is_flipped {
  transform: rotateY(-180deg);
}
.card_face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  /* padding: 1rem; */
  box-shadow: 0 3px 18px 3px rgba(0, 0, 0, 0.2);
}
.card_front > .card_content {
  width: 100%;
  height: 100%;
  background: var(--dark) url('../assets/images/icon_back.png') no-repeat center;
  object-fit: contain;
}
.card_back {
  background-color: var(--light);
  transform: rotateY(180deg);
}
.card_back > .card_content {
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
  background-image: url('../assets/images/10.png');
}
</style>
