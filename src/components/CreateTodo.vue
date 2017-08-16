<template>
    <div class="column is-one-third">
        <div class="container is-fluid">
            <div class="list-header">
                <div class="field">
                    <label class="label">Create a Task</label>
                    <p class="control">
                        <input class="input" type="text" placeholder="To do Title" v-model="titleText" :class="{validate: required}">
                        <span v-show="required" class="error">The title is required.</span>
                    </p>
                </div>
                <div class="field">
                    <label class="label">Description</label>
                    <p class="control">
                        <textarea class="textarea"  type="text" placeholder="Task Description" v-model="projectText"></textarea>
                    </p>
                </div>
                <div class="field">
                <label class="label">Importance</label>
                    <div class="control">
                        <div class="select">
                            <select v-model="projectImportance">
                                <option value="0">Select dropdown</option>
                                <option value="1">somewhat important</option>
                                <option value="2">important</option>
                                <option value="3">very important</option>
                            </select>
                        </div>
                    </div>
                </div>
                <div class="field">     
                    <label class="label">Due date</label>
                    <p class="control">
                        <input class="input" type="date" placeholder="Date" v-model="dueDate" required>
                    </p>
                    <br>
                    <p class="control">
                        <button class="button is-primary disable" @click="sendForm()">Add</button>
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    export default {  
        data () {
            return {
                titleText: '',
                projectText: '',
                dueDate:'',
                projectImportance:'',
                required:false
            }
        },
        methods:{
            sendForm(){
                if(this.titleText.length > 0){
                    const title = this.titleText;
                    const description = this.projectText;
                    const date = this.dueDate;
                    const importance = this.projectImportance;
                    this.$emit('create-todo',{
                        title,
                        description,
                        date,
                        done: false,
                        importance,
                        isEditing: false
                    });
                    this.titleText = '';
                    this.projectText = '';
                    this.dueDate = '';
                    this.projectImportance = '';
                    this.required = false;
                }else{
                    this.required = true;
                }
            }
        }
    }

</script>
<style>
    .validate{
        border-color: red !important;
    }
    .error{
        color:red !important;
    }
    input{
        max-width:100%;
    }
</style>



