<template>
    <div>
        <!-- completed flag -->
        <div :class="{completed: todo.done}">
            <div class="card" v-show="!todo.isEditing">
                <header class="card-header" v-show="todo.done">
                    <p class="card-header-title">
                        Completed
                    </p>
                    <a class="card-header-icon" v-show="todo.done">
                        <span class="icon">
                            <i class="fa fa-undo" aria-hidden="true" @click="incompleteTodo(todo)"></i>
                        </span>
                    </a>                 
                </header>
                <!-- end of complete flag -->
                <!-- Card that shows when isEditing is false -->
                <header>
                    
                </header>
                <div class="card-content">
                    <p class="title">
                        {{todo.title}}
                    <span class="icon" v-show="!todo.done" v-if="todo.importance == 1">
                    <i class="fa fa-exclamation important" aria-hidden="true"></i>
                    </span>
                    <span class="icon" v-show="!todo.done" v-if="todo.importance == 2">
                    <i class="fa fa-exclamation important" aria-hidden="true"></i>
                    <i class="fa fa-exclamation important" aria-hidden="true"></i>
                    </span>
                    <span class="icon" v-show="!todo.done" v-if="todo.importance == 3">
                    <i class="fa fa-exclamation important" aria-hidden="true"></i>
                    <i class="fa fa-exclamation important" aria-hidden="true"></i>
                    <i class="fa fa-exclamation important" aria-hidden="true"></i>
                    </span>                           
                    </p>    
                    <p class="subtitle">
                        {{todo.description}}
                    </p>                                       
                    <p v-show="!todo.done" v-if="todo.date.length > 0">Due date:</p>
                    <p class="subtitle" type="calendar" >
                        {{todo.date}}   
                    </p>
                </div>
                <footer class="card-footer">
                    <p class="card-footer-item" v-show="!todo.done">
                        <span>
                            <a v-on:click="completeTodo(todo)">Complete</a>
                        </span>
                    </p>
                    <p class="card-footer-item" v-show="!todo.done">
                        <span>
                            <a v-on:click="willEdit(todo)">Edit</a>                     
                        </span>
                    </p>
                    <p class="card-footer-item">
                        <span>
                            <a v-on:click="deleteTodo(todo)">Delete</a>
                        </span>
                    </p>
                </footer>
            </div>
        </div>
        <!-- this is the card that will show when isEditing is true -->
        <div class="card" v-show="todo.isEditing">
            <div class="card-content">
                <input class="title" id="focus" :value="this.todo.title" v-on:input="updateTitle($event.target.value)">                 
                <p class="control subtitle"><input class="subtitle" :value="todo.description" v-on:input="updateDescription($event.target.value)" style="width: 100%"></p>
                <p class="control"><input class="input" type="date" :value="todo.date" v-on:input="updateDate($event.target.value)"></p>
            </div>
            <footer class="card-footer">
                <p class="card-footer-item" v-show="!todo.done">
                    <span>
                        <a v-show="todo.done" v-on:click="completeTodo(todo)" disable>Complete</a>
                    </span>
                </p>
                <p class="card-footer-item" v-show="!todo.done">
                    <span>
                        <a v-on:click="doneEditing(todo)">Done Editing</a>                      
                    </span>
                </p>
                <p class="card-footer-item">
                    <span>
                        <a v-on:click="deleteTodo(todo)">Delete</a>
                    </span>
                </p>
            </footer>
        </div>
    </div>  
</template>

<script>
    export default {
        props: ['todo'],
        data () {
            return {
                editState:'Edit',
            }
        },
        methods:{       
            deleteTodo(todo){
                this.$parent.$parent.$emit('delete-todo', todo);
            },
            completeTodo(todo){
                this.$parent.$parent.$emit('complete-todo', todo);
            },
            incompleteTodo(todo){
                this.$parent.$parent.$emit('incomplete-todo', todo);
            },
            willEdit(todo){
                this.$parent.$parent.$emit('editing-todo', todo);
            },
            doneEditing(todo){
                this.$parent.$parent.$emit('done-editing', todo);
                this.$parent.$parent.$emit('update-todo', todo);            
            },
            updateTitle:function (value) {
                this.todo.title = value
                this.$emit('input', this.todo.title)        
            },
            updateDescription:function (value) {
                this.todo.description = value
                this.$emit('input', this.todo.description)
            },
            updateDate:function (value) {
                this.todo.date = value
                this.$emit('input', this.todo.date)
            },
        }
    };
</script>

<style>
    .important{
    font-size: 28px !important;
    color:red !important;
}
</style>
