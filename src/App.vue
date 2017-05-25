<template>
  <div id="app">
    <Todo owner="Nick's"></Todo>
  </div>
</template>

<script>
  import Todo from './Todo.vue'

  export default {
    name: 'app',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App'
      }
    },
    components: {
      Todo
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Lato:400,700,900');

  * {
    box-sizing: border-box;
  }

  *:focus {
    outline: 1px dashed #4a4a4a;
  }

  html {
    color: #4a4a4a;
    font-family: 'Lato', sans-serif;
  }

  html,
  body,
  #app {
    height: 100%;
    width: 100%;
  }

  #app {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .u-visually-hidden {
    position: absolute;
  	clip: rect(1px, 1px, 1px, 1px);
  	padding:0;
  	border:0;
  	height: 1px;
  	width: 1px;
  	overflow: hidden;
  }
</style>
