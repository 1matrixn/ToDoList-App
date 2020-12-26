<template>
  <div id="app">

    <div class="wrapper">
      <div class="header">
        <input class="input-line" v-model="inputField" v-on:keyup.enter="addTodo" placeholder="Что нужно сделать?" />
        <button class="button-line" @click="addTodo"><i class="fas fa-plus"></i></button>
      </div>


      <ul id="list" type="none">
        <li v-for="todo in todoList">
          <div class="element-todo" >
            <input class="input-element" type="checkbox" v-on:change="toggle(todo)" v-bind:checked="todo.complete">
            <del class="span-element" v-if="todo.complete">
              {{ todo.name }}
            </del>
            <span class="span-element" v-else>
              {{ todo.name }}
            </span>
            <span class="span-click" @click="deleteTodo(todo)"><i class="fas fa-trash-alt"></i></span>
          </div>
        </li>
      </ul>
    </div>

  </div>

</template>

<script>
import Vue from 'vue';

import test from './components/test';

export default {
  name: 'app',
  components: {
     test
 },
  methods: {
    addTodo: function(todo) {
      todo = this.inputField;
      if (todo)
        this.todoList.push({name: todo, complete: false});
      else
        alert( "Введите корректное значение!" );
      this.inputField = '';
      console.log(this.todoList);
   },
   deleteTodo: function(todo) {
      var index = this.todoList.indexOf(todo);
      this.todoList.splice(index, 1);
      console.log(this.todoList);
   },
   toggle: function(todo) {
      todo.complete = !todo.complete;
   }
 },
  data () {
    return {
      inputField: '',
      todoList: []
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }
  .wrapper {
    width: 920px;
    margin: 0 auto;
  }
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  ul li {
    cursor: pointer;
    position: relative;
    padding: 12px 8px 12px 0;
    background: #eee;
    font-size: 18px;
    transition: 0.2s;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

  ul li:nth-child(odd) {
    background: white;
  }

  ul li:hover {
    background: #ddd;
  }

  ul li.checked {
    background: #888;
    color: #fff;
    text-decoration: line-through;
  }
  ul li.checked::before {
    content: '';
    position: absolute;
    border-color: #fff;
    border-style: solid;
    border-width: 0 2px 2px 0;
    top: 10px;
    left: 16px;
    transform: rotate(45deg);
    height: 15px;
    width: 7px;
  }

  .header:after {
    content: "";
    display: table;
    clear: both;
  }

  input {
    width: 89%;
    padding: 10px;
  }

  .button-line {
    padding: 10px;
    background: white;
    float: right;
    text-align: center;
    font-size: 16px;
    cursor: pointer;
    transition: 0.3s;
  }

  ul {
    margin: 0;
    padding: 0;
  }

  .input-line {
    font-size: 4em;
    border: 3px solid black;
  }

  .button-line {
    font-size: 5em;
    border: 3px solid white;
  }

  .input-element {
    width: 10%;
    height: 100px;
    float: left;
  }

  .span-element {
    width: 80%;
    float: left;
    font-size: 5em;
  }

  .span-click {
    width: 10%;
    font-size: 5em;
  }

  .element-todo {
    height: 100px;
    width: 100%;
  }
</style>
