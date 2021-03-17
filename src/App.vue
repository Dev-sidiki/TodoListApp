<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <todo-list></todo-list>
    <router-view/>
  </div>
</template>

<script>
import Todos from './components/Todos'
export default {
  components: { Todos }
}
</script>

<style>
*{
  box-sizing: border-box;
}
.container{
  max-width: 800px;
  margin: 0 auto;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
 /* text-align: center;*/
  color: #2c3e50;
  margin-top: 60px;
  font-size: 28px;
}
.logo{
  display: block;
  margin : 35px auto ;
  height: 75px;
}
</style>
