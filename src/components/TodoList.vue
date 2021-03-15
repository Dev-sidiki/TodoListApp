<template>
    <div>
     <input type="text" class="todo-input" placeholder="Que voulez-vous faire?"
      v-model="newTodo" @keyup.enter="addTodo">
      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
          <div class="todo-item-left">
              <input type="checkbox" v-model="todo.completed">
              <div v-if="!todo.editing" @dblclick="editTodo(todo)"
               class="todo-item-label" :class="{ completed:
               todo.completed }">{{ todo.title }}</div>
              <input v-else class="todo-item-edit" type="text"
               v-model="todo.title" @blur="doneEdit(todo)"
                @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
          </div>
             <div class="remove-item" @click="removeTodo(index)">
                 &times;
             </div>
         </div>

         <div class="extra-container">
             <div><label><input type="checkbox">Check All</label></div>
             <div>{{ remaining }} items left</div>
         </div>
      </div>
</template>>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      todos: [
        {
          'id': 1,
          'title': 'Programmer',
          'completed': false,
          'editing': false,
        },
        {
          'id': 2,
          'title': 'dormir',
          'completed': false,
          'editing': false,
        },
      ]
    }
  },

  computed:{
      remaining() {
          return this.todos.filter(todo => !todo.completed).length
      }
  },

  directives: {
      focus: {
          inserted: function (el){
              el.focus()
          }
      }
  },

  methods: {
      addTodo(){

         this.todos.push({
                 id: this.idForTodo,
                 title: this.newTodo,
                 completed: false,
         })
         this.newTodo = ''
         this.idForTodo++
      },
      editTodo(todo){
          this.beforeEditCache = todo.title
          todo.editing = true
      },

      doneEdit(todo){
          if (todo.title.trim() == ' ') {
              todo.title = this.beforeEditCache
          }
          todo.editing = false
      },

      cancelEdit(todo) {
          todo.editing = false
      },

      removeTodo(index) {
          this.todos.splice(index, 1)
      }
  }
}
</script>

<style>
    .todo-input{
        width: 100%;
        padding: 10px 10px;
        font-size: 18px;
        margin-bottom: 16px;
    }
    
    .todo-item {
        margin-bottom: 12px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .remove-item {
        cursor: pointer;
        margin-left: 14px;
    }

    .todo-item-edit {
        font-size: 24px;
        color: #2c3e58;
        margin-left: 12px;
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        font-family: 'Avenir', Arial, Helvetica, sans-serif;
    }

    .completed {
        text-decoration: line-through;
        color: grey;
    }

    .extra-container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-size: 16;
        border-top: 1px solid lightgrey;
        padding-top: 14px;
        margin-bottom: 14px;
    }

    .active {
        background: lightgreen;
    }
</style>
