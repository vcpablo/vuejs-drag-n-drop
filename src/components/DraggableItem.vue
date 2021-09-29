<template>
  <span
    draggable="true"
    @dragstart="handleDragStart"
  >
    <slot />
  </span>
</template>

<script>
export default {
  name: 'DraggableItem',
  props: ['transferData'],
  setup(props)  {
    const handleDragStart = event => {
      event.dataTransfer.setData('value', JSON.stringify(props.transferData))
    }

    return { handleDragStart }
  }
}
</script>
