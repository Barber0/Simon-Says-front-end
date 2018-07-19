<template>
<div>
	<div class="tl">
		<Icon type="flag" size="30"></Icon>
		<span>推广</span>
	</div>
	<div>
		<News v-for="(item, index) in rklist.slice(0,4)" :key="index" :info="item" />
	</div>
</div>
</template>

<script>
import News from './News'
export default{
	name:'news-panel',
	data(){
		return{
			rklist:[{}]
		}
	},
	methods:{
		addNews(newInfo){
			let vm = this
			vm.news.push(newInfo)
		},
		alarm(){
			alert(JSON.stringify(this.news))
		}
	},
	components:{
		News
	}
}
</script>

<style>

</style>
