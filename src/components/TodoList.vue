<template>
    <div class="column is-one-third">
        <section class="section no-padding">
            <div class="container">
                <h1 class="title is-small">To do List:</h1>
                <h2 class="subtitle">
                    <p class="tasks">Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
                    <p class="tasks">Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
                </h2>
            </div>
        </section>
        <br>
        <transition-group name="fade">
            <todo v-for="todo in todos" v-if="!todo.done" :todo.sync="todo" v-bind:key="todo['.key']"></todo>
            <todo v-for="todo in todos" v-if="todo.done" :todo.sync="todo" v-bind:key="todo['.key']"></todo>
        </transition-group>
    </div>
</template>

<script>
    import Todo from './Todo.vue'
    export default {

        props:['todos'],

        components:{
            Todo
        },
        methods:{

        }
    }
</script>

<style>
    .fade-enter-active, .fade-leave-active {
        transition: opacity .2s
    }
    .fade-enter, .fade-leave-to {
        opacity: 0
    }
</style>

