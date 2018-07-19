<template>
<div>
	<HeadBar ref="head-bar" :user="user" />
	<div class="head-wrapper">
		<MainPanel ref="mainPanel" />
	</div>
	<div class="body-wrapper">
		<BodyPanel ref="bdPanel" :videos="vdList" :pagi="pagi" />
	</div>
</div>
</template>

<script>
import HeadBar from '@/components/HeadBar'
import MainPanel from './MainPanel'
import BodyPanel from './BodyPanel'
import './index.less'
export default {
	name:'index',
	data(){
		return{
			pagi:{
				page:1,
				size:16,
				total:0
			},
			vdList:[{}],
			rankList:[[{}],[{}]],
			user:{}
		}
	},
	methods:{
		fakeLogin(){
      let vm = this
      vm.$axios.get('/api/user/fake/login/').then(rsp=>{
        vm.key = rsp.data.data
        console.log(vm.key)
      }).catch(err=>{
        alert(err)
      })
    },
		fetchUserInfo(){
			let vm = this
			vm.$axios.get('/api/user/').then(rsp=>{
				if(rsp.data.code==200) vm.user = rsp.data.data
					else console.log(rsp)
			}).catch(err=>{
				console.log(err)
			})
		},
		fetchVideos(){
			let vm = this
			vm.$axios.get('/api/file/video/all/createAt?page='+vm.pagi.page+'&size='+vm.pagi.size).then(rsp=>{
				if(rsp.data.code==200){
					vm.vdList = rsp.data.data.content
					vm.pagi.total = rsp.data.data.totalElements
				}else console.log(rsp)
			}).catch(err=>{
				console.log(err)
			})
		},
		changePage(name){
			let vm = this
			vm.pagi.page = name
			vm.fetchVideos()
		},
		fetchRankList(cls){
			let vm = this
			vm.$axios.get('/api/file/video/all/view?page='+cls+'&size=8').then(rsp=>{
				if(rsp.data.code==200) {
					// vm.rankList[cls-1] = rsp.data.data.content
					if(cls==1) vm.$refs.bdPanel.$refs.ranklist.list = rsp.data.data.content
						else if(cls==2) vm.$refs.mainPanel.$refs.newsPanel.rklist = rsp.data.data.content
				}else console.log(rsp)
			}).catch(err=>{
				console.log(err)
			})
		}
	},
	mounted(){
		let vm = this
		// vm.fakeLogin()
		vm.fetchUserInfo()
		vm.fetchVideos()
		vm.fetchRankList(1)
		vm.fetchRankList(2)
	},
	components:{
		HeadBar,
		MainPanel,
		BodyPanel
	}
}
</script>

<style>
</style>
