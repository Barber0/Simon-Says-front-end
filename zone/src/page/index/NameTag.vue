<template>
<div class="name-card" style="padding:0;">
  <div class="hd-banner" style="background-image:url(/banner.jpg)">
    <div class="basic-info">
      <div class="col1">
        <img :src="user.header">
      </div>
      <div class="col2">
        <div class="uname one-line">{{user.nickname}}</div>
        <div class="intro one-line">{{user.intro}}</div>
      </div>
    </div>
  </div>
  <div class="tool-bar">
    <Menu mode="horizontal" theme="light" active-name="upload" @on-select="toolBar">
      <MenuItem name="upload">
        <Button type="success">上传视频</Button>
      </MenuItem>
      <MenuItem name="info">
        <Icon type="person" />
        修改信息
      </MenuItem>
      <MenuItem name="chpass">
        <Icon type="stats-bars" />
        更改密码
      </MenuItem>
      <MenuItem name="logout">
        <Icon type="stats-bars" />
          注销
      </MenuItem>
      <!-- <Submenu name="rank">
        <template slot="title">
            <Icon type="stats-bars"></Icon>
            视频排序
        </template>
        <MenuItem name="3-1">上传时间</MenuItem>
        <MenuItem name="3-2">播放热度</MenuItem>
      </Submenu> -->
    </Menu>
  </div>

  <Modal
      v-model="infoDialog"
      title="个人信息修改"
      @on-ok="submitUpdate">
      <InfoDialog ref="infoD" />
  </Modal>
  <Modal
      v-model="uploadDialog"
      title="视频上传"
      @on-ok="submitVideo">
      <VideoDialog ref="videoD" />
  </Modal>
  <Modal 
    v-model="chPassDialog"
    title="修改密码"
    @on-ok="submitPassCh">
    <div style="padding:20px">
      <div>
        <Input v-model="pass.origin" placeholder="请输入原密码"></Input>
      </div>
      <div style="margin-top:10px">
        <Input v-model="pass.new_pass" placeholder="请输入新密码"></Input>
      </div>
      <div style="margin-top:10px">
        <Input v-model="pass.check_pass" placeholder="请输入验证密码"></Input>
      </div>
    </div>
  </Modal>
</div>
</template>

<script>
import InfoDialog from '@/page/index/InfoDialog'
import VideoDialog from '@/page/index/VideoDialog'
export default{
  name:'NameTag',
  props:['user','bkUp'],
  data(){
    return{
      bn1Style:{
        backgroundImage:"url(/spa/zone/banner.jpg)",
      },
      infoDialog:false,
      uploadDialog:false,
      chPassDialog:false,
      pass:{
        origin:'',
        new_pass:'',
        check_pass:''
      }
    }
  },
  methods:{
    upload(){
      alert("你好")
    },
    toolBar(name){
      let vm = this
      let infoD = vm.$refs.infoD
      switch(name){
        case "info":
          vm.infoDialog = true
          infoD.user = vm.bkUp
          break
        case "upload":
          vm.uploadDialog = true
          break
        case "logout":
          location = '/logout/'
          break
        case "chpass":
          vm.chPassDialog = true
          break
        default:
          alert(name)
          break
      }
    },
    submitUpdate(){
      let vm = this
      vm.$axios.put('/api/user/',vm.bkUp).then(rsp=>{
        console.log(rsp)
        if(rsp.data.code==200) {
          vm.user = rsp.data.data
          vm.$Notice.success({
            title:'个人信息修改成功',
            desc:'信息修改成功'
          })
        }
      }).catch(err=>{
        console.log(err)
      })
    },
    submitPassCh(){
      let vm = this
      vm.$axios.post('/api/user/ch/',vm.pass).then(rsp=>{
        if(rsp.data.code==200) vm.$Notice.success({title:'密码修改成功'})
          else {
            vm.$Notice.error({title:'修改失败'})
            console.log(rsp)
          }
      }).catch(err=>{
        vm.$Notice.error({title:'修改失败'})
        console.log(err)
      })
    },
    abc(str){alert(str)},
    submitVideo(){
      let vm = this
      let reqBody = vm.$refs.videoD.video
      vm.$axios.post('/api/file/video/',reqBody).then(rsp=>{
        if(rsp.data.code==200){
          vm.$Notice.success({
            title:'投稿成功',
            desc:'恭喜恭喜，又多了一件新作品'
          })
          vm.$parent.$refs.vdList.fetchVideos()
        }else vm.$Notice.error({
          title:'投稿失败',
          desc:rsp.data.msg
        })
      }).catch(err=>{
        console.log(err)
      })
    }
  },
  mounted(){
    let vm = this
  },
  components:{
    InfoDialog,
    VideoDialog
  }
}
</script>

<style>
</style>
