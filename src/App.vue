<template>
  <div id="app">
    <header class="app-header">
      <input type="text" v-model="newTask" class="txt-add">
      <button @click="createNewTask" class="btn-kanban">Add Task</button>
	</header>
	<div class="pipeline-container">
      <pipeline
   	    v-for="c in columns"
	    :key="c"
	    :title="c"
	    :list="tasks"
	    @newStatus="updateTask"
	    @deleteTask="deleteTask"
	  />
	</div>
  </div>
</template>

<script>
import Pipeline from './components/Pipeline';
export default {
  name: 'app',
  components: {
	  Pipeline
  },
  data () {
    return {
	  newTask: '',
	  columns: ['ToDo', 'Doing', 'Done'],
	  tasks: [
		  {
			title: 'Sample',
			status: 'ToDo',
		  }
	  ]
    }
  },
  methods: {
	  createNewTask() {
		  if (this.newTask) {
			  if (this.tasks.find(t => t.title === this.newTask)) {
				  alert('There is already a task with this content!');
				  return;
			  }
			  this.tasks.push({
				  title: this.newTask,
				  status: 'ToDo'
			  });
			  this.newTask = '';
		  }
	  },
	  updateTask(payload) {
		  const taskToUpdate = this.tasks.find(t => t === payload.task);
		  taskToUpdate.status = payload.newStatus;
	  },
	  deleteTask(task) {
		  console.log('Deleting this')
		  const index = this.tasks.indexOf(task);
		  console.log(task, index)
		  this.tasks.splice(index, 1);
	  }
  }
}
</script>

<style scoped>
* {
  font-family: 'Avenir', 'Sans-Serif';
}
.pipeline-container {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
    height: 80vh;
	justify-content: space-evenly;
	align-items: flex-start;
	margin-top: 20px;
}

.btn-kanban {
	border: 0;
	border-radius: 2px;
	font-weight: 300;
	font-size: 10pt;
	color: #FFFFFF;
	padding: 9px 8px;
    background-color: #658AE9;
}

.app-header {
	width: 100%;
	text-align: center;
}

.txt-add {
	width: 30%;
}


</style>
