<template>
	<div>
		<h3>用户添加</h3>
		<form >
			<input type="" v-model="user.name" id="" value="" />
			<input type="" v-model="user.age" id="" value="" />
			<input type="" v-model="user.bir" id="" value="" />
			<input @click="saveUserInfo" value="提交"/>
		</form>
	</div>
</template>

<script>
	export default {
		name: "Useradd",
		data(){
			return{
				user:{}
			}
		},
		methods:{
			saveUserInfo(){
				// console.log(this.user)
				this.$http.post("http://rs.nbsod.com/api/index/add",this.user).then(res=>{
					console.log(res)
					if(res.status == 200){
						this.$router.push("/user");   //切换路由
					}
				})
			}
		}
	}
</script>

<style>
	input{
		border: 1px solid #e6e6e6;
	}
</style>
