<template>
	<div>
		<todos-header></todos-header>
		<radio-selection v-on:radio-click="radioChange"></radio-selection>
		<todos-table v-bind:filteredTodos="computedTodos" v-on:status-click="statusChange" v-on:delete-click="todoDelete"></todos-table>
		<todo-addition v-on:add-click="taskAdd"></todo-addition>
	</div>
</template>

<script>
	import todosHeader from './todos-header.vue';
	import radioSelection from './radio-selection.vue';
	import todosTable from './todos-table.vue';
	import todoAddition from './todo-addition.vue';

	export default {

		components:{
			'todos-header':todosHeader,
			'radio-selection':radioSelection,
			'todos-table':todosTable,
			'todo-addition':todoAddition,
		},

		data:function(){
			return {
				todos:[],				
				temporaryStoredTodos:[],
				currentRadio:"all",
			};
		},

		methods:{
			taskAdd:function(task){
				const todo = {taskName:task, status:"doing"};
				this.todos.push(todo);
				this.createId();
			},
			createId:function(){
				this.todos.forEach((element, index) => {
					element.id = index + 1;});
			},
			statusChange:function(elementId){
				if(this.todos[elementId-1].status === "doing"){
					this.todos[elementId-1].status = "done";
				} else {
					this.todos[elementId-1].status = "doing";
				}
			},
			todoDelete:function(elementId){
				this.todos.splice(elementId-1, 1);
				this.createId();
			},			
			radioChange:function(radio){
				this.currentRadio = radio;
			},
		},

		computed:{
			computedTodos:function(){
				if(this.currentRadio === "all"){
					return this.todos;
				}
				return this.todos.filter(element => {
					return element.status === this.currentRadio;
				});
			},
		},		
	}
</script>