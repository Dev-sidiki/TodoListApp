/* eslint-disable */
<template>
  <div>
    <input type="text" class="new-todo" placeholder="Ajouter une tâche" v-model="newTodo"
     @keyup.enter="addTodo">
    <transition-group  enter-active-class="animatedfadeInUp" leave-active-class="animated fadeOutDown">
    <todo-item v-for="(todo,index) in todosFiltered" :key="todo.id" :todo="todo" :index="index"
     :checkAll="!itemRestant" @todoRemoved="removeTodo" @finishedEdit="finishedEdit">
    </todo-item>
    </transition-group>
    <div class="extra-container">
      <div><label>
        <input type="checkbox" :checked="!itemRestant" @change="checkAllTodos"> Tous coher</label>
      </div>
      <div>{{remaining}} taches restantes</div>
   </div>
    <div class="extra-container">
      <div>
      <button :class="{ active: filter =='all'}" @click="filter ='all'"> Toutes les tâches</button>
      <button :class="{ active: filter =='active'}" @click="filter ='active'"> Taches Inachevées</button>
      <button :class="{ active: filter =='completed'}" @click="filter ='completed'">Taches accomplies</button>
      </div>
      <div>
        <button v-if="showClearComplitedButton"
        @click="clearCompleted">Clear Completed</button>
      </div>
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'
export default {
  name: 'todo-list',
  components: {
    TodoItem
  },
  data () {
    return {
      todos: [{
        'id': 1,
        'title': 'nouvelle tâche1',
        'completed': false,
        'editing': false
      },
      {
        'id': 2,
        'title': 'nouvelle tâche2',
        'completed': false,
        'editing': false
      }
      ],
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      filter: 'all'
    }
  },
  computed: {
    remaining () {
      return this.todos.filter(todo => !todo.completed).length
    },
    itemRestant () {
      return this.remaining !== 0
    },
    todosFiltered () {
      if (this.filter === 'all') {
        return this.todos
      } else if (this.filter === 'active') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'completed') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    },
    /** Methode qui permet d'afficher les tâches à effacer */
    showClearComplitedButton () {
      return this.todos.filter(todo => todo.completed).length > 0
    }
  },
  methods: {
    addTodo () {
      if (this.newTodo.trim().length === 0) {
        return
      }
      /* On verifie que l'utilisateur entre bien un text . */
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false
      })
      this.newTodo = ''
      this.idForTodo++
    },
    /* Methode de supression  */
    removeTodo (index) {
      this.todos.splice(index, 1)
    },
    /* eslint-disable */
    /** Methode qui permet de cocher toutes les tâches */
    checkAllTodos () {
      this.todos.forEach((todo) => todo.completed = 
      event.target.checked)

    },
      /** Methode qui permet  d'effacer les tâches accomplies */
    clearCompleted () {
       this.todos = this.todos.filter(todo => !todo.completed)
    },
    finishedEdit(data) {
      this.todos.splice(data.index, 1, data.todo)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.1/animate.min.css");
.todo-list {
  widows: 100%;
  padding: 10px 10px;
  font-size: 14px;
  margin-bottom: 10px;
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
.todo-item-left {
  display: flex;
  align-items: center;
}
.todo-item-label{
  padding: 10px;
  border: 1px solid white;
  margin-left: 12px;

}
.todo-item-edit{
  font-size:24px;
  color:rgb(255, 136, 0);
  margin-left: 12px;
  width:100%;
  padding:10px;
  border: 1px solid #ccc;
  font-family: 'Avenir',Arial, Helvetica, sans-serif;
}
.completed {
  text-decoration: line-through;
  color: green;
}
.extra-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 14px;
  border-bottom: 1px solid lightgray;
  padding-top: 14px;
  margin-bottom: 14px;
}
button {
  font-size: 14px;
  background-color:aquamarine;
  appearance: none;
}
.active {
  background:lightgreen;
}

.fade-leave-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
