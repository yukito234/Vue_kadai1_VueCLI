<template>
	<div>			
		<label v-for="radioElement in radioTypes" v-bind:key="radioElement.value">
			<input type="radio" v-model="radioType" v-bind:value="radioElement.value">{{ radioElement.label }}
		</label>
    </div>
</template>

<script>
	export default {
		data:function(){
			return {
				radioTypes:[
					{ value: "all", label: 'すべて'},
					{ value: "doing",  label: '作業中'},
					{ value: "done",  label: '完了'}
				],
				radioType:"all",
			};
		},
		
		watch:{
			radioType:function(){				
				this.$emit("radio-click", this.radioType);
			},
		},
	}
</script>