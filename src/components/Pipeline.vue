<template>
  <div class="pipeline">
    <header>
      <h3> {{ title }} </h3>
    </header>
	<div class="card-container">
      <task-card
	    v-for="task in myList"
	    :key="task"
	    :task="task"
	    @statusChanged="statusChanged"
	    @deleteTask="emitDelete"
	  />
    </div>
  </div>
</template>

<script>
import TaskCard from './TaskCard';
export default {
  name: 'Pipeline',
  props: {
	title: {
	  type: String,
	  required: true
	},
	list: {
		type: Array,
		required: true
	}
  },
  components: {
	  TaskCard
  },
  computed: {
	  myList() {
		  return this.list.filter(t => t.status === this.title)
	  }
  },
  methods: {
	  statusChanged(payload) {
		  if (payload.task.status !== payload.newStatus) {
			  this.$emit('newStatus', payload)
		  }
	  },
	  emitDelete(payload) {
		  this.$emit('deleteTask', payload);
	  }
  }
}
</script>

<style scoped>
.pipeline {
  background-color: #F6F6F6;
  border-radius: 2px;
  box-shadow: 2px 2px 8px 1px #ccc;
  height: 80vh;
  width: 25vw;
  padding: 2px 2px 8px 2px;
}

.pipeline header {
	text-align: center;
	padding: 1px 3px 1px 3px;
	line-height: 1.6px;
	border-bottom: 1px solid #AFADAD;
}

.pipeline header h3 {
	font-size: 14pt;
	font-weight: 500;
}

.pipeline .card-container {
    overflow-y: auto;
    height: 90%;
}
</style>
