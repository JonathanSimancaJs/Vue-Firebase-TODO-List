<template>
	<div class="column is-one-third">
		<div class="container is-fluid">
			<div class="list-header">
				<div class="field">
					<label class="label">Create a Task</label>
					<p class="control">
						<input class="input" type="text" placeholder="To do Title" v-model="titleText">
					</p>
				</div>
				<div class="field">
					<label class="label">Description</label>
					<p class="control">
						<textarea class="textarea"  type="text" placeholder="Task Description" v-model="projectText"></textarea>
					</p>
				</div>
				<div class="field">	  	
					<label class="label">Due date</label>
					<p class="control">
						<input class="input" type="date" placeholder="Date" v-model="dueDate">
					</p>
					<br>
					<p class="control">
						<button class="button is-primary" @click="sendForm()">Add</button>
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
      dueDate:''
	}
  },
  methods:{
  	sendForm(){
  		if(this.titleText.length > 0 && this.projectText.length > 0 && this.dueDate.length > 0){
  			const title = this.titleText;
  			const description = this.projectText;
  			const date = this.dueDate;
  			this.$emit('create-todo',{
  				title,
  				description,
  				date,
  				done: false,
  				isEditing: false
  			});
  		this.titleText = '';
        this.projectText = '';
        this.dueDate = '';
  		}
  	}
  }
}	
</script>



