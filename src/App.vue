<template>
  <div id="app">
   <div class="container is-fluid">
    <hero></hero>
    <div class="columns">
      <create-todo v-on:create-todo="createTodo"></create-todo>
      <todo-list v-bind:todos="todos" v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-on:incomplete-todo="incompleteTodo" v-on:editing-todo="editingTodo" v-on:done-editing="doneEditingTodo" v-on:update-todo="updateTodo"></todo-list>
      <shia-labeouf></shia-labeouf>
    </div>
  </div>
</div>
</template>

<script>

  import router from './router'
  import firebase from 'firebase'
  import Hero from './components/Hero.vue'
  import sweetalert from 'sweetalert'
  import CreateTodo from './components/CreateTodo.vue'
  import TodoList from './components/TodoList.vue'
  import ShiaLabeouf from './components/ShiaLabeouf.vue'

  let config = {
    apiKey: "AIzaSyCiWNrRyDLTzXlznBYPfCjeO36fnkN3miM",
    authDomain: "todo-firebase-a1453.firebaseapp.com",
    databaseURL: "https://todo-firebase-a1453.firebaseio.com",
    projectId: "todo-firebase-a1453",
    storageBucket: "todo-firebase-a1453.appspot.com",
    messagingSenderId: "1001872278589"  
  }
  const todosRef = firebase.initializeApp(config).database().ref('todos')

  export default {
    name: 'app',
    components:{
      Hero,
      TodoList,
      CreateTodo,
      ShiaLabeouf
    },
    firebase:{
      todos: todosRef,
    },
    methods: { 
      createTodo(newTodo){
        todosRef.push(newTodo)
      },
      updateTodo(todo){
        todosRef.child(todo['.key']).child('title').set(todo.title);
        todosRef.child(todo['.key']).child('description').set(todo.description);
        todosRef.child(todo['.key']).child('date').set(todo.date);
      },
      completeTodo:function(todo){
        todosRef.child(todo['.key']).child('done').set(true);
      },
      incompleteTodo:function(todo){
        todosRef.child(todo['.key']).child('done').set(false);
      }, 
      deleteTodo: function (todo) {
        sweetalert({
          title: 'Are you sure?',
          text: 'This Todo will be permanently deleted!',
          showCancelButton: true,
          confirmButtonColor: '#DD6B55',
          confirmButtonText: 'Yes, delete it!',
          closeOnConfirm: false,
        },
        () => {
          todosRef.child(todo['.key']).remove();
          sweetalert('Deleted!', 'Success!');
        }  
        )
      },
      editingTodo:function(todo){
        todosRef.child(todo['.key']).child('isEditing').set(true)
      },
      doneEditingTodo:function(todo){
        todosRef.child(todo['.key']).child('isEditing').set(false)
      },           
    },
  }

</script>

<style lang="scss">

  @import "../node_modules/bulma/bulma.sass";
  .list-header{
   max-width:450px;
 }
 figure{
  width:268px;
  height:200px;
  margin-left: 2vw;
}
.no-padding{
  padding:0;
  margin: 0 auto;
}
body{
  padding: 0 20px;
}
.completed .title, .completed .subtitle{
  color: #a8a8a8 !important;
}
.card-footer{
  margin-bottom: 1.25vh !important;
}
</style>
