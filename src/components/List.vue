<template>
  <ul class="list-group">
    <li class="list-group-item d-flex justify-content-between rounded-0" v-for="item in items" :key="item.id">
      {{ item.name }}
      <button class="btn btn-danger btn-sm" @click="onUnselect(item)">
        <i class="bi-trash d-flex" />
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'DraggableList',
  props: ['items', 'onUnselect']
}
</script>