<template>
  <div
    @dragenter="onDragEnter"
    @dragover="onDragOver"
    @dragleave="onDragLeave"
    @drop="onDrop"
  >
    <slot />
  </div>
</template>

<script>
export default {
  name: 'DroppableItem',
  props: [
    'onDragEnter',
    'onDragOver',
    'onDragLeave',
    'onDrop'
  ]
}
</script>
