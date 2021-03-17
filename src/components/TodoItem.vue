<template>
    <div class="toto-item">
        <div class="todo-item-left">
            <input type="checkbox" v-model="completed" @change="doneEdit">
            <!-- L'utilisation des methode de modification (double click sur un item pour avoir la possiblité de modifier, touche echap pour annuler la modification -->
            <div v-if="!editing" @dblclick="editTodo"
            class="todo-item-label" :class="{completed : completed}">{{title}}</div>
            <input v-else class="todo-item-edit" type="text" v-model="title" @blur="doneEdit"
            @keyup.enter="doneEdit" @keyup.esc="cancelEdit" v-focus>
        </div>
        <div class="remove-item" @click="removeTodo(index)">
        &times;
        </div>
    </div>
</template>
<script>

export default {
  name: 'todo-item',
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    checkAll: {
      type: Boolean,
      required: true
    }

  },
  data () {
    return {
      'id': this.todo.id,
      'title': this.todo.title,
      'completed': this.todo.completed,
      'editing': this.todo.editing,
      'beforEditCache': ''

    }
  }, /**  Watcher qui permet d'observer si tous les items sont cocheés */
  watch: {
    checkAll () {
      /* if (this.checkAll) {
        this.completed = true
      } else {
        this.completed = this.todo.completed
      } */
      this.completed = this.checkAll ? true : this.todo.completed
    }
  },
  /**  Methode removeTodo eventListener qui permet au parent(todos) d'écouter une acttion sur les item todo */
  methods: {
    removeTodo (index) {
      this.$emit('todoRemoved', index)
    },
    /* Methode de modification */
    editTodo () {
      this.beforeEditCache = this.title
      this.editing = true
    },
    /** Methode fin de modification  qui permet de notifier le parent sur la fin de modification */
    doneEdit (t) {
      if (this.title.trim() === '') {
        this.title = this.beforeEditCache
      }
      this.editing = false
      this.$emit('finishedEdit', {
        'index': this.index,
        'todo': {
          'id': this.id,
          'title': this.title,
          'completed': this.completed,
          'editing': this.editing
        }
      })
    },
    /** Methode qui permet d'annuler une modification en  */
    cancelEdit () {
      this.title = this.beforeEditCache
      this.editing = false
    }
  }
}
</script>
