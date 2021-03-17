<template>
    <div>
      <button :class="{ active: filter =='all'}" @click="changeFilter('all')"> Toutes les tâches</button>
      <button :class="{ active: filter =='active'}" @click="changeFilter('active')"> Taches Inachevées</button>
      <button :class="{ active: filter =='completed'}" @click="changeFilter('completed')">Taches accomplies</button>
    </div>
</template>

<script>
import EventBus from './event-bus'
export default {
  name: 'todo-filtered',
  data () {
    return {
      'filter': 'all'
    }
  },
  methods: {
    changeFilter (filter) {
      this.filter = filter
      EventBus.$emit('filterChanged', filter)
    }
  }
}
</script>
