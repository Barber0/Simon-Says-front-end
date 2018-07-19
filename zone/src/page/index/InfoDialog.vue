<template>
<div class="dialog">
  <Row class="rw">
    <Col span="3">
      Id：
    </Col>
    <Col span="8">
      <span v-text="user.id"></span>
    </Col>
    <Col span="3" offset="1">
      用户名：
    </Col>
    <Col span="8">
      <span v-text="user.username"></span>
    </Col>
  </Row>
  <Row class="rw">
    <Col class="lb" span="3">
      昵称
    </Col>
    <Col span="8">
      <Input v-model="user.nickname" placeholder="请输入您的昵称"></Input>
    </Col>
    <Col class="lb" span="3" offset="1">
      邮箱
    </Col>
    <Col span="8">
      <Input v-model="user.email" placeholder="请输入您的邮箱"></Input>
    </Col>
  </Row>
  <Row class="rw">
    <Col class="lb" span="3">
      自我介绍
    </Col>
    <Col span="20">
      <Input v-model="user.intro" placeholder="请输入您的自我介绍"></Input>
    </Col>
  </Row>
  <Row class="rw">
    <Col span="3" class="lb">
      上传头像
    </Col>
    <Col span="8">
      <Upload ref="uploader" action="/api/file/upload/img/" name="file" :show-upload-list="true" :on-success="finishUpload">
        <Button type="ghost" icon="ios-cloud-upload-outline">Upload files</Button>
      </Upload>
    </Col>
  </Row>
</div>
</template>

<script>
export default{
  name:'InfoDialog',
  data(){
    return{
      rsp:{},
      fi:{},
      list:[],
      user:{}
    }
  },
  methods:{
    finishUpload(rsp,fi,list){
      let vm = this
      if(rsp.code==200){
        vm.$Notice.success({
          title: '头像上传成功',
          desc: '新形象，新印象',
        });
        vm.user.header = rsp.data
      }else{
        vm.$Notice.error({
          title:'文件上传错误',
          desc:rsp.msg
        })
      }
    },
  },
  mounted(){
  }
}
</script>

<style>

</style>
