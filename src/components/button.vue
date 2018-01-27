<template>
	<div>
		<button @click="loginEvent()">{{title}}</button>
	</div>
</template>

<script>
	export default{
		data:function(){
			return{
				title:this.name || '确认'
			}
		},
		props:['name'],
		methods:{
			loginEvent:function(){
				this.$emit('confirm')
			}
		}
	}
	
</script>

<style>
	div{
		margin-top: 24px;
		
	}
	button{
		width: 92%;
		height: 60px;
		border: none;
		border-radius: 17px;
		margin: 0px auto;
		background: #B92C28;
		color: white;
		/*margin: 0 20px;*/
		margin-left: 20px;
		font-size: 20px;
	}
</style>