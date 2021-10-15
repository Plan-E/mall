<template>
	<div>
		<h3>用户列表</h3>
		<table border="1">
			<tr>
				<td>编号</td>
				<td>姓名</td>
				<td>年龄</td>
				<td>生日</td>
				<td>操作</td>
			</tr>
			<tr v-for="user in users" :key="user.id">
				<td>{{user.id}}</td>
				<td>{{user.name}}</td>
				<td>{{user.age}}</td>
				<td>{{user.bir}}</td>
				<td>
					<a :href="'#/user/edit?id='+user.id">修改</a>
					<a href="javascript:;" @click="del(user.id)">删除</a>
				</td>
			</tr>
		</table>
		<a href="#/user/add">添加</a>
		<router-view></router-view>
	</div>
</template>

<script>
	export default {
		name: "User",
		data(){
			return{
				users: []
			}
		},
		methods:{
			findAll(){   //查询所有
				this.$http.get("http://rs.nbsod.com/api/index").then((res)=>{
					console.log(res.data.data.user)
					this.users = res.data.data.user;
				})
			},
			del(id){  //删除
				this.$http.get("http://rs.nbsod.com/api/index/delete?id="+id).then(res=>{
					console.log(res.data.data.user)
					this.findAll()
				})
			}
		},
		components:{},
		created(){
			this.findAll()
		},
		watch:{
			// 监听路由变化
			$route: {
				handler: function(val, oldVal){
					// console.log(val)
					if(val.path == '/user'){
						this.findAll()
					}
				}
			}
		}
	}
</script>

<style>
</style>