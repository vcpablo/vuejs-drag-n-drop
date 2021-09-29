<template>
  <span
    @dragover="handleOnDragOver"
    @dragleave="onDragLeave"
    @drop="onDrop"
  >
    <slot />
  </span>
</template>

<script>
export default {
  name: 'DroppableItem',
  props: [
    'onDragOver',
    'onDragLeave',
    'onDrop'
  ],
  setup(props) {
    const handleOnDragOver = event => {
      event.preventDefault()
      props.onDragOver && props.onDragOver(event)
    }

    return { handleOnDragOver }
  }
}
</script>
