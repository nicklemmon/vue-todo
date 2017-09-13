<template>
  <div class="todo" :class="classes">
    <div class="todo__header">{{ owner }} to-do list</div>

    <div class="todo__blk">
      <label class="u-visually-hidden" for="enter-todo-item">Enter to-do item</label>

      <div class="todo__input-btn-grp">
        <input v-model="todoText" v-on:keyup.enter="addItem" class="todo__input" type="text" id="enter-todo-item" name="enter-todo-item" placeholder="e.g., wash the car" aria-describedby="todo__error-msg">

        <button v-on:click="addItem" class="todo__input-btn" tabindex="0">
          <span class="u-visually-hidden">Add Item</span>
        </button>
      </div>

      <span class="error-msg" id="todo__error-msg">{{ errorText }}</span>
    </div>

    <ul class="todo__list">
      <transition-group name="todo__list-item">
        <li v-for="(todoItem, index) in todoItems" v-on:click="checkItem( index, todoItem )" v-bind:key="todoItem" class="todo__list-item" :class="{ checked : todoItem.isChecked }" role="button" tabindex="0" href="javascript:void(0);">
          {{ todoItem.text }}
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
        // 1. add the appropriate class to the clicked element
        // 2. fire `removeIndex()` when `transitioned` event fires
        console.log( todoItem );
        todoItem.isChecked = !todoItem.isChecked;

        let removeIndex = () => {
          this.todoItems.splice( index, 1 );
        }

        removeIndex();
      }
    }
  }
</script>

<style>
  .todo {
    background: #fff;
    box-shadow: 0 4px 8px 0 #dbdbdb;
    height: auto;
    width: 400px;
  }

  .todo__header {
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

  .todo__blk {
    padding: 25px;
  }

  .todo__list {
    border-top: 1px solid #f1f1f1;
    overflow: hidden;
    padding-bottom: 25px;
    -webkit-margin-after: 0;
    -webkit-margin-before: 0;
    -webkit-padding-start: 0;
  }

  .todo__list-item {
    align-items: center;
    border-bottom: 1px solid #f1f1f1;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    list-style-type: none;
    height: 50px;
    padding: 0 25px;
    position: relative; /* allows absolute positioning within */
    transition: background 0.4s ease-in-out;
  }

  .todo__list-item-enter-active,
  .todo__list-item-leave-active {
    transition: opacity 0.4s ease-in-out,
                transform 0.4s ease-in-out;
  }

  .todo__list-item-enter,
  .todo__list-item-leave-active {
    opacity: 0;
    transform: translateX(-100%);
  }

  .todo__list-item:after {
    background: #fff;
    border: 1px solid #dbdbdb;
    border-radius: 50%;
    content: '';
    display: block;
    height: 25px;
    width: 25px;
  }

  .todo__list-item:hover,
  .todo__list-item:focus {
    background: #f1f1f1;
  }

  .todo__list-item:focus {
    outline: 0;
  }

  .todo__input-btn-grp {
    display: flex;
  }

  .todo__input {
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

  .todo__input-btn {
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

    .todo__input-btn:hover {
      background: #3b73b3;
    }

    .todo__input-btn:after,
    .todo__input-btn:before {
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

    .todo__input-btn:after {
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
