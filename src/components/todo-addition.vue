<template>
	<div>
		<h2>新規タスクの追加</h2>
		<input type="text" v-model="taskInput">
		<button  v-on:click="add">追加</button>
	</div>
</template>

<script>
	export default {
		data:function(){
			return {
				taskInput: "",
			};
		},
		methods:{
			add:function(){
				this.$emit("add-click", this.taskInput);
			},
		},
	}
</script>