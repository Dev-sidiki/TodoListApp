<template>
     <div>{{remaining}} taches restantes</div>
</template>

<script>
export default {
  name: 'todo-restant',
  props: {
    remaining: {
      type: Number,
      required: true
    }
  }
}
</script>
