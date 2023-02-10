<script setup>
  import {ref,computed} from 'vue';
  let id = 0;
  const tempText = ref("");
  const hideFinishedTask = ref(false);
  const todos = ref([
    {id:id++,text:"Some Todos1",done:false},
    {id:id++,text:"Some Todos2",done:false},
    {id:id++,text:"Some Todos3",done:false},
    ]);
  function addTask() {
    if (tempText.value != "") {
      todos.value.push({id:id++,text:tempText.value,done:false});
      tempText.value = "";
    }
  }
  function removeTask(someTodo) {
    todos.value = todos.value.filter((todo) => todo != someTodo);
  }
  const todosFormatted = computed(()=> !hideFinishedTask.value ? todos.value : todos.value.filter((todo)=>todo.done != true));
</script>
<template>
  <div class="wrapper">
    <header>
    <h1>To-Do List</h1>
    </header>
    <section>
      <input v-model="tempText" type=text placeholder="Enter Task">
      <button @click="addTask">Add Task</button>
      <ul>
        <li v-for="todo in todosFormatted" :id="todo.id">
        <input type="checkbox" v-model="todo.done">
        <span :class="{finishedTask:todo.done}">{{todo.text}}</span>
        <button @click="removeTask(todo)">x</button>
      </li>
      <button @click="hideFinishedTask = !hideFinishedTask">{{hideFinishedTask ? "Show Finished Task" : "Hide Finished Task"}}</button>
      </ul>
    </section>
  </div>
</template> 

<style>
  .wrapper {
    margin-block:24px;
    flex: 1 0 auto;
    max-width: 1280px;
    width:100%;
    height:inherit;
    display: flex;
    flex-direction: column;
    border-radius: 36px;
    background-color:white;
  }
  header {
    background-color:#42D392;
    border-radius: 24px 24px 0 0 ;
    color:white;
/*    width: 100%;*/
  }
  h1 {
    text-align: center;
    font-size: 5rem;
    font-weight: 800;
  }
  section {
    padding: 1rem 2rem;
    display:flex;
    flex-direction:column;
    justify-content:flex-start;
/*    align-items:flex-start;*/
    flex:1 1 auto;
  }
  section > :nth-child(-n + 2) {
    height: 70px;
    margin:6px;
    border-radius: 12px;
  }
  input {
    font-size: 2rem;
    font-weight: 600; 
    text-align:center;
/*    background-color:white;*/
/*    border: 3px solid rgb(211, 211, 211);*/
  }
  button {
    color: #454545;
    background-color:lightgray;
    border: 4px solid transparent;
    font-size:2rem;
  }
  button:hover {
    background-color:#42D392;
  }
  button:active {
    background-color:white;
    border:4px solid #42D392;
  }
  li {
    font-weight:700;
    list-style: none;
    display:flex;
    align-items:center;
    gap:12px;
/*    justify-content:center;*/
  }
  li span {
    font-size: 3rem;
  }
  li input {
    height:35px;
    width:35px;
  }
  .finishedTask {
    text-decoration: line-through;
  }
</style>