<template>
  <div class="task-card">
    <header>
    <button @click="emitDelete(task)" class="close-button">X</button>
    </header>
	<div class="task-body">
      <p> {{ task.title }} </p>
      <button @click="emitNewStatus('ToDo')" class="btn-task todo">To do</button>
      <button @click="emitNewStatus('Doing')" class="btn-task doing">Doing</button>
      <button @click="emitNewStatus('Done')" class="btn-task done">Done</button>
	</div>
  </div>
</template>

<script>
export default {
  name: 'app',
  props: {
	task: {
	  type: Object,
	  required: true
	}
  },
  methods: {
	  emitNewStatus(newStatus) {
		  this.$emit('statusChanged', { task: this.task, newStatus});
	  },
	  emitDelete(task) {
		  if (confirm('Are you sure you want to delete it?')) {
		    this.$emit('deleteTask', { task });
		  }
	  }

  }
}
</script>

<style scoped>

.task-card {
  background-color: #FFFFFF;
  margin: 20px 10px 0px 10px;
  box-shadow: 2px 2px 8px 1px #ccc;
  border-radius: 2px;
  width: 95%;
}

.task-card header {
	background-color: #EEEEEE;
	text-align: right;
	padding: 3px;
}

.task-card .task-body {
	padding: 8px;
}

.btn-task {
	border: 0;
	border-radius: 2px;
	font-weight: 300;
	font-size: 10pt;
	color: #FFFFFF;
	padding: 3px 8px;
}

.task-card .task-body .todo {
  background-color: #658AE9;
}

.task-card .task-body .doing {
  background-color: #FF9839;
}

.task-card .task-body .done {
  background-color: #8DD148;
}

.close-button {
    background-color: #FF7070;
	border: 0;
	border-radius: 50%;
	width: 15px;
	height: 15px;
	padding: 0 0 0 0;
	text-align: center;
	font-size: 8pt;
}
</style>
