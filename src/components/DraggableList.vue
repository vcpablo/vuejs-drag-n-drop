<template>
  <ul class="list-group">
    <DraggableItem v-for="item in items" :key="item.id" :id="item.id" :transferData="item">
      <li class="list-group-item">
        <i class="DraggableList__drag-handler bi-three-dots-vertical" />
        <span class="mx-3">
          {{ item.name }}
        </span>
      </li>
    </DraggableItem>
  </ul>
</template>

<script>
import DraggableItem from './DraggableItem'

export default {
  name: 'DraggableList',
  components: {
    DraggableItem
  },
  props: ['columns', 'items']
}
</script>

<style scoped>
  .DraggableList__drag-handler {
    width: 10px;
    cursor: grab;
  }

  .DraggableList__drag-handler:active {
    cursor: grabbing;
  }
</style>