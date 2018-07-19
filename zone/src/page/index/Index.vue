<template>
<div>
  <HeadBar :user="user" />
  <div v-if="user.id!=undefined" class="zone-panel">
    <NameTag ref="nameTag" :user="user" :bkUp="bkUp" />
    <VideoList ref="vdList" :user="user" />
  </div>
  <div v-else class="zone-panel">
    <Card style="text-align:center">
      <h2>您尚未登录</h2>
    </Card>
  </div>
</div>
</template>

<script>
import HeadBar from '@/components/HeadBar'
import NameTag from '@/page/index/NameTag'
import VideoList from '@/page/index/VideoList'
import '@/page/index/zone.less'
export default{
  name:'Index',
  data(){
    return{
      user:{},
      key:'',
      bkUp:{}
    }
  },
  components:{
    HeadBar,
    NameTag,
    VideoList
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
        if(rsp.data.code==200) {
          vm.user = rsp.data.data
          vm.bkUp = JSON.parse(JSON.stringify(vm.user))
          console.log(vm.user)
        }else console.log(rsp.data.msg)
      }).catch(err=>{
        console.log(err)
      })
    }
  },
  mounted(){
    let vm = this
    // vm.fakeLogin()
    vm.fetchUserInfo()
  }
}
</script>

<style>
</style>
