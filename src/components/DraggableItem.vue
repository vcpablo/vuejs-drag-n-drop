<template>
  <span
    :transfer-data="transferData"
    draggable="true"
    @dragstart="handleDragStart"
    @drag="onDrag"
    @dragenter="onDragEnter"
    @dragover="onDragOver"
    @dragleave="onDragLeave"
    @dragend="onDragEnd"
  >
    <slot />
  </span>
</template>

<script>
export default {
  name: 'DraggableItem',
  props: [
    'transferData',
    'onDragStart',
    'onDrag',
    'onDragEnter',
    'onDragOver',
    'onDragLeave',
    'onDragEnd'
  ],
  setup(props)  {
    const handleDragStart = event => {
      event.dataTransfer.setData('Text', JSON.stringify(props.transferData))
      props.onDragStart && props.onDragStart(event)
    }

    return { handleDragStart }
  }
}
</script>
