<template>
	<div>
		<h3>修改用户</h3>
		<form >
			<input type="" v-model="user.name" id="" value="" />
			<input type="" v-model="user.age" id="" value="" />
			<input type="" v-model="user.bir" id="" value="" />
			<input @click="edit"  value="提交"/>
		</form>
	</div>
</template>

<script>
	export default {
		name: "UserEdit",
		data(){
			return{
				user:{
					id:''
				}
			}
		},
		methods:{
			findOne(){			
				this.$http.get("http://rs.nbsod.com/api/index/edit?id="+this.user.id).then(res=>{
					console.log(res.data.data.user)
					this.user = res.data.data.user
					
				})
			},
			edit(){
				this.$http.post("http://rs.nbsod.com/api/index/update",this.user).then(res=>{
					console.log(res)
					if(res.status == 200){
						this.$router.push("/user");   //切换路由
					}
				})
			},
		},
		created(){
			
			this.user.id = this.$route.query.id
			console.log(this.$route.query.id)
			this.findOne()
		},
	}
</script>

<style>
	input{
		border: 1px solid #e6e6e6;
	}
</style>
