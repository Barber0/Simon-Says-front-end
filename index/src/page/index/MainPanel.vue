<template>
<div class="main-panel">
	<div>
		<div class="head-panel">
			<Gallery ref="galy" />
		</div>
		<div>
			<NewsPanel class="news-panel" ref="newsPanel" />
		</div>
	</div>
</div>
</template>

<script>
import Gallery from './Gallery'
import NewsPanel from './NewsPanel'
export default{
	name:'main-panel',
	data(){
		return{
			value1:0,
		}
	},
	methods:{
		show(){let vm = this}
	},
	mounted(){
		let vm = this
	},
	components:{
		Gallery,
		NewsPanel,
	}
}
</script>

<style>

</style>
