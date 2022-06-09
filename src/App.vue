<template>
	<div id="app">
		<h1>Tarefas</h1>
		<TaskProgress :percent="percentTasks" /> 
		<NewTask @taskAdded="addTask($event)" />
		<TaskList :tasks="tasks" 
			@deleteTask="deleteTask($event)" 
			@changeStatusTask="changeStatusTask($event)"
		/>
	</div>
</template>

<script>
	import TaskList from './components/TaskList.vue'
	import NewTask from './components/NewTask.vue'
	import TaskProgress from './components/TaskProgress.vue'

	export default {
		components:{ TaskList, NewTask, TaskProgress},
		data() {
			return {
				tasks: []
			}
		},
		computed: {
			percentTasks() {
				const total = this.tasks.length
				const done = this.tasks.filter(t=> !t.pending).length

				return Math.round(done / total * 100) || 0
			}
		},
		watch:{
			tasks: {
				deep: true,
				handler(){
					localStorage.setItem('tasks', JSON.stringify(this.tasks))
				}	
			}
		},
		methods: {
			addTask(task){
				//verificando se a tarefa já existe 
				const taskName = t => t.name === task.name
				//filtrando os elementos do array e verificando se realmente 
				//náo existe elementos com mesmo nome retornando verdadeiro ou falso
				const reallyNewTask = this.tasks.filter(taskName).length == 0

				//verificando se o elemento é novo e adicionando no array
				//a nova tarefa passada pelo componente filho NewTask
				if(reallyNewTask){
					this.tasks.push({
						name: task.name,
						//por padrão o atributo pending será true
						pending: task.pending || true
					})
				}
			},
			deleteTask(task){
				//removendo com indice passado via evento
				// this.tasks.splice(i, 1)

				//removendo com a task passada via evento
				const i = this.tasks.indexOf(task)
				this.tasks.splice(i, 1)

			},
			changeStatusTask(i){
				this.tasks[i].pending = !this.tasks[i].pending
			}
		},
		created(){
				const json = localStorage.getItem('tasks')
				const array =   JSON.parse(json)
				this.tasks = Array.isArray(array) ? array : []
			}
	}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
