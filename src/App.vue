<template>
  <div class="container mt-3">
    <DraggableUsersSelect v-model="selectedUsers" :users="users"/>
    <DraggableBalls />
  </div>
</template>

<script>
import { ref } from 'vue'
import DraggableUsersSelect from '@/components/DraggableUsersSelect'
import DraggableBalls from '@/components/DraggableBalls'

export default {
  name: 'App',
  components: {
    DraggableUsersSelect,
    DraggableBalls
  },
  setup() {
    const users = [
      {
        id: 1,
        name: 'Jon Doe',
        order: 0
      },
      {
        id: 2,
        name: 'Jane Doe',
        order: 1
      },
      {
        id: 3,
        name: 'Bob Taylor',
        order: 2
      },
      {
        id: 4,
        name: 'Jack Spice',
        order: 3
      },
      {
        id: 5,
        name: 'Mary Jane',
        order: 4
      }
    ]

    const selectedUsers = ref([])

    return { users, selectedUsers }
  }
}
</script>