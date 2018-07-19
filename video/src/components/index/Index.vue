<template>
<div>
  <HeadBar :user="user" />
  <div class="top-panel">
    <TopPanel ref="topPanel" :video="video" />
  </div>
  <div class="main-panel">
    <div class="ltpn">
      <VdPanel ref="vdPanel" :video="video[0]" :user="user" />
    </div>
    <div class="rtpn">
      <Table :columns="danCol" :data="danRow" height="470" size="small"></Table>
    </div>
  </div>
  <div class="foot-panel">
    <div>
      <Row>
        <Col span="8">
          <h1>视频简介</h1>
        </Col>
        <Col span="5" offset="11">
          <Button type="primary">点赞</Button>
          <Button type="warning">收藏</Button>
          <Button type="success">分享</Button>
        </Col>
      </Row>
    </div>
    <div class="desc" v-text="video[0].description"></div>
  </div>
</div>
</template>

<script>
import HeadBar from '@/components/headbar/HeadBar'
import TopPanel from '@/components/index/TopPanel'
import VdPanel from '@/components/index/VdPanel'
import Utils from '@/components/utils'
import './index.less'
export default{
  name:'Index',
  data(){
    return{
      user:{},
      video:[{},{}],
      damaku:[{}],
      danCol:[
        {
          title:'内容',
          key:'text',
        },
        {
          title:'进度',
          key:'time',
        }
      ],
      danRow:[{}]
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
          else {
            vm.user.id = -1
            vm.user.nickname = '游客'
            console.log(rsp)
          }
      }).catch(err=>{
        vm.user.nickname = '游客'
        vm.user.id = -1
        console.log(err)
      })
    },
    fetchVideo(){
      let vm = this
      let vid = vm.$route.params.vid
      vm.$axios.get('/api/file/video/'+vid).then(rsp=>{
        if(rsp.data.code==200) {
          vm.video = rsp.data.data
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
    vm.fetchVideo()
    console.log(vm.user)
  },
  components:{
    HeadBar,
    TopPanel,
    VdPanel
  }
}
</script>

<style>
</style>
