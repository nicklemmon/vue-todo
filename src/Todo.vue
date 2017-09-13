<template>
  <div class="todo" :class="classes">
    <div class="header">{{ owner }} to-do list</div>

    <div class="content">
      <label class="u-visually-hidden" for="enter-todo-item">Enter to-do item</label>

      <div class="input-btn-grp">
        <input v-model="todoText" v-on:keyup.enter="addItem" class="input" type="text" id="enter-todo-item" name="enter-todo-item" placeholder="e.g., wash the car" aria-describedby="error-msg">

        <button v-on:click="addItem" class="input-btn" tabindex="0">
          <span class="u-visually-hidden">Add Item</span>
        </button>
      </div>

      <span class="error-msg" id="error-msg">{{ errorText }}</span>
    </div>

    <ul class="list">
      <transition-group name="list-item">
        <li v-for="(todoItem, index) in todoItems" v-on:click="checkItem( index, todoItem )" v-bind:key="todoItem" class="list-item" :class="{ checked : todoItem.isChecked }" role="button" tabindex="0" href="javascript:void(0);">
          {{ todoItem.text }}

          <span class="check" role="presentation"></span>
        </li>
      </transition-group>
    </ul>
  </div>
</template>

<script>
  import Alert from './Alert.vue'

  export default {
    name: 'Todo',
    props: ['classes', 'owner'],
    data() {
      return {
        todoItems: [],
        todoText: '',
        errorText: ''
      }
    },
    methods: {
      addItem: function( event ) {
        if ( this.todoText.length > 0 ) {
          this.todoItems.push({ text: this.todoText });
          this.todoText = '';
        } else {
          this.errorMsg( 'Sorry! You will need to enter something to add to the list.' );
        }
      },
      errorMsg: function( msgContent ) {
        this.errorText = msgContent;
      },
      checkItem: function( index, todoItem ) {
        todoItem.isChecked = !todoItem.isChecked;

        let removeIndex = () => {
          this.todoItems.splice( index, 1 );
        }

        removeIndex();
      }
    }
  }
</script>

<style scoped>
  .todo {
    background: #fff;
    box-shadow: 0 4px 8px 0 #dbdbdb;
    height: auto;
    width: 400px;
  }

  .header {
    align-items: center;
    background: #fafafa;
    color: #30383e;
    display: flex;
    font-size: 14px;
    height: var(--spacing--md);
    justify-content: center;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .content {
    padding: 25px;
  }

  .list {
    border-top: 1px solid #f1f1f1;
    overflow: hidden;
    padding-bottom: 25px;
    -webkit-margin-after: 0;
    -webkit-margin-before: 0;
    -webkit-padding-start: 0;
  }

  .list-item {
    align-items: center;
    border-bottom: 1px solid #f1f1f1;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    list-style-type: none;
    height: 50px;
    outline-offset: -1px;
    padding: 0 25px;
    position: relative; /* allows absolute positioning within */
    transition: background 0.4s ease-in-out;
  }

  .list-item-enter-active {
    animation: slideRight 0.4s ease-in-out;
  }

  .list-item-leave-active {
    animation: slideLeft 0.4s ease-in-out;
    animation-delay: 0.2s;
  }

  .list-item-leave-active .check:after {
    transform: rotate(45deg) scale(1);
  }

  .list-item:hover {
    background: #f1f1f1;
  }

  .check {
    align-items: center;
    background: #fff;
    border: 1px solid #dbdbdb;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    padding: 12.5px;
    position: relative; /* allows absolute positioning within */
  }

  /* this is the actual check */
  .check:after {
    background: transparent;
    content: '';
    left: 35%;
    height: 50%;
    width: 25%;
    border-right: 2px solid #7ed321;
    border-bottom: 2px solid #7ed321;
    position: absolute;
    top: 12.5%;
    transform: rotate(45deg) scale(0);
    transition: transform 0.2s ease-in-out;
  }

  .input-btn-grp {
    display: flex;
  }

  .input {
    border: 1px solid #f1f1f1;
    border-radius: 5px 0 0 5px;
    border-right: 0; /* not necessary when button present */
    box-shadow: inset 0 5px 12.5px rgba(241, 241, 241, 0.4);
    font-size: 14px;
    height: 50px;
    padding: 25px;
    width: 100%;
    -webkit-appearance: none;
  }

  .input-btn {
    align-items: center;
    background: #4990e2;
    border: 1px solid #3b73b3;
    border-radius: 0 5px 5px 0;
    color: #fff;
    cursor: pointer;
    display: flex;
    justify-content: center;
    padding: 25px;
    position: relative; /* allows absolute positioning within */
    width: 50px;
    transition: background 0.3s ease-in-out;
  }

    .input-btn:hover {
      background: #3b73b3;
    }

    .input-btn:after,
    .input-btn:before {
      content: '';
      background: white;
      border-radius: 2px;
      display: block;
      height: 3px;
      left: 30%;
      position: absolute;
      width: 40%;
      top: 48%;
    }

    .input-btn:after {
      transform: rotate(90deg);
    }

  /* Keyframes and animations */
  @keyframes slideRight {
    0% {
      transform: translateX(-100%);
    }

    50% {
      transform: translateX(3%);
    }

    100% {
      transform: translateX(0);
    }
  }

  @keyframes slideLeft {
    0% {
      transform: translateX(0%);
    }

    50% {
      transform: translateX(3%);
    }

    100% {
      transform: translateX(-100%);
    }
  }
</style>
