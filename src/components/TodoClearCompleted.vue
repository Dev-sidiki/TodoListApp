<template>
    <button v-if="showClearComplitedButton"
        @click="clearCompleted">Clear Completed</button>
</template>
<script>
import EventBus from './event-bus'
export default {
  name: 'todo-clear-completed',
  props: {
    showClearCompletedButton: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    clearCompleted () {
      EventBus.$emit('clearCompletedTodos')
    }
  }
}
</script>
