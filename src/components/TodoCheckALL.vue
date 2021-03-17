<template>
     <div>
        <label>
            <input type="checkbox" :checked="!itemRestant" @change="allChecked"> Tous coher
        </label>
      </div>
</template>

<script>
import EventBus from './event-bus'
export default {
  name: 'todo-check-all',
  props: {
    itemRestant: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    allChecked () {
      EventBus.$emit('checkAllChanged', this.itemRestant)
    }
  }
}
</script>
