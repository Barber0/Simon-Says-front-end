<template>
<div>
	<div class="header">
		<div class="hd-tl">
			<div class="tl"><i>Simon Says</i></div>
			<div style="float:left;margin-left:20px;font-size:22px;padding:5px;"><i>最燃最皮的弹幕社区</i></div>
			<div v-if="user.id!=undefined" class="us">
				<Dropdown>
					<div>
						<div class="un">{{user.nickname}}</div>
						<img :src="user.header">
					</div>
					<DropdownMenu slot="list">
						<DropdownItem><a href="/zone/"><b>个人中心</b></a></DropdownItem>
            <DropdownItem><a href="/logout/"><b>注销</b></a></DropdownItem>
					</DropdownMenu>
				</Dropdown>
			</div>
			<div v-else class="nous">
				<a href="/login/">
					<Button type="success" size="large">登录</Button>
				</a>
				<a href="/register/">
					<Button type="warning" size="large">注册</Button>
				</a>
			</div>
		</div>
	</div>
</div>
</template>

<script>
import './headbar.less'
export default{
	name:'headbar',
	props:['user'],
	data(){
		return{
		}
	},
	methods:{
		show(){
			this.$axios.get("/api/alpha/").then((rsp)=>{
			// this.$axios.get("/api/test/?page=0").then((rsp)=>{
				alert(rsp.data)
				console.log(rsp)
			}).catch((err)=>{
				alert(err)
				console.log(err)
			})
		},
	}
}
</script>

<style scoped>

</style>