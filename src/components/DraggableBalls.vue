<template>
  <div>
    <DraggableItem v-for="ball in availableBalls" :key="ball.id" :transferData="ball">
      <span class="circle">
        {{ ball.id }}
      </span> 
    </DraggableItem>
    <hr />
    <DroppableItem v-bind="{ onDragOver, onDragLeave, onDrop }">
      <span :class="droppableItemClass">
        <span class="circle" v-for="ball in selectedBalls" :key="ball.id">
          {{ ball.id }}
        </span>
      </span>
    </DroppableItem>
  </div>
</template>

<script>
import { differenceBy } from 'lodash/fp'
import { computed, ref } from 'vue'

import DraggableItem from './DraggableItem'
import DroppableItem from './DroppableItem'

export default {
  name: 'DraggableBalls',
  components: {
    DraggableItem,
    DroppableItem
  },
  setup() {
    const balls = [ { id: 1 }, { id: 2 }, { id: 3 } ]

    const selectedBalls = ref([])
    const isDroppableItemActive = ref(false)

    const availableBalls = computed(() => differenceBy('id', balls, selectedBalls.value))
    const droppableItemClass = computed(() => ['square', isDroppableItemActive.value && 'hover'])

     const onDragOver = () => {
       isDroppableItemActive.value = true
     }

     const onDragLeave = () => isDroppableItemActive.value = false

     const onDrop = event => {
        const ball = JSON.parse(event.dataTransfer.getData('value'))
        selectedBalls.value = [
          ...selectedBalls.value,
          ball
        ]
        isDroppableItemActive.value = false
     }

     return { availableBalls, selectedBalls, droppableItemClass, onDragOver, onDragLeave, onDrop }
  }
}
</script>

<style>
.circle {
  width: 50px;
  height: 50px;
  border-radius: 50%; 
  border: 1px solid red;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-right: 5px;
}

.square {
  display: inline-block;
  width: 250px;
  height: 250px;
  border: 1px dashed black;
  padding: 10px;
}

.hover {
  background-color: rgb(172, 255, 158);
}
</style>