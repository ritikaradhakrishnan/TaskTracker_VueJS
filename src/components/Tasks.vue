<template>
    <div :key="task.id" v-for="task in tasks">
      <Task
        @toggle-reminder="$emit('toggle-reminder', task.id)"
        @delete-task="$emit('delete-task', task.id)"
        :task="task"
      />
    </div>
  </template>



//we want to take in the task array from App.vue as a prop
<script>
import Task from './Task'
export default {
  name: 'Tasks',
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  emits: ['delete-task', 'toggle-reminder'],
}
</script>

