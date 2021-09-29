<template>
  <div>
    <h1>Drag Users to Select</h1>
    <div class="row">
      <div class="col">
        <div class="card">
          <div class="card-header">
            Users
          </div>
           <div class="card-body">
              <DraggableList v-if="filteredUsers.length > 0" v-bind="{ columns, items: filteredUsers }" />
              <div v-else class="alert alert-warning">
                All users have been selected
              </div>
           </div>
          </div>
      </div>
      <div class="col">
        <div class="card">
          <div class="card-header">
            Selected Users
          </div>

            <DroppableItem v-bind="{ onDragOver, onDragLeave, onDrop }" class="DroppableItem" :class="droppableItemClass">
              <div class="card-body">
                <List v-if="selectedUsers.length > 0" :items="selectedUsers" :onUnselect="onUnselect"/>
                <div v-else class="text-center">Drop users here to select</div>
              </div>
            </DroppableItem>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import { differenceBy, filter } from 'lodash/fp'

import DraggableList from './DraggableList'
import DroppableItem from './DroppableItem'
import List from './List'

export default {
  name: 'DraggableUsersSelect',
  components: {
    DraggableList,
    DroppableItem,
    List
  },
  props: ['modelValue', 'users'],
  setup(props, { emit }) {
    const isDroppableItemActive = ref(false)

    const droppableItemClass = computed(() => [
      isDroppableItemActive.value && 'alert-warning'
    ])

    const selectedUsers = computed({
      get: () => props.modelValue,
      set: value => emit('update:modelValue', value)
    })

    const filteredUsers = computed(() => differenceBy('id', props.users, selectedUsers.value))

    const onDragOver = () => {
      isDroppableItemActive.value = true
    }

    const onDragLeave = () => isDroppableItemActive.value = false

    const onDrop = () => {
      const selectedUser = JSON.parse(event.dataTransfer.getData('Text'))
      selectedUsers.value = [...selectedUsers.value, selectedUser]
      isDroppableItemActive.value = false
    }

    const onUnselect = item => selectedUsers.value = filter(({ id }) => id !== item.id,selectedUsers.value)

    return { filteredUsers, selectedUsers, droppableItemClass, onDragOver, onDragLeave, onDrop, onUnselect }
  }
}
</script>

