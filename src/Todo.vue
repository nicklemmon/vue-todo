<template>
  <div class="todo" :class="classes">
    <div class="todo__header">{{ owner }} to-do list</div>

    <div class="todo__blk">
      <label class="u-visually-hidden" for="enter-todo-item">Enter to-do item</label>

      <div class="todo__input-btn-grp">
        <input v-model="todoText" v-on:keyup.enter="addItem" class="todo__input" type="text" id="enter-todo-item" name="enter-todo-item" placeholder="e.g., wash the car">

        <button v-on:click="addItem" class="todo__input-btn" tabindex="0">
          <span class="u-visually-hidden">Add Item</span>
        </button>
      </div>
    </div>

    <ul class="todo__list">
      <li v-for="todoItem in todoItems" v-bind:class="{ active: is-active }" class="todo__list-item" role="button" tabindex="0">
        {{ todoItem.text }}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'Todo',
    props: ['classes', 'owner'],
    data() {
      return {
        todoItems: [],
        todoText: ''
      }
    },
    methods: {
      addItem: function( event ) {
        this.todoItems.push({ text: this.todoText });
        this.todoText = '';
      }
    }
  }
</script>

<style>
  .todo {
    background: #fff;
    box-shadow: 0 4px 6px 0 #dbdbdb;
    height: auto;
    width: 400px;
  }

  .todo__header {
    align-items: center;
    background: #fafafa;
    color: #30383e;
    display: flex;
    font-size: 14px;
    height: 50px;
    justify-content: center;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .todo__blk {
    padding: 25px;
  }

  .todo__list {
    border-top: 1px solid #f1f1f1;
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
    transition: background 0.3s ease-in-out;
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

  .todo__list-item.is-checked:after {
    background: #f1f1f1;
  }

  .todo__list-item:hover {
    background: #f1f1f1;
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
</style>
