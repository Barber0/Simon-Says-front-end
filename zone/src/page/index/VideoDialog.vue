<template>
<div class="dialog">
  <Row class="rw">
    <Col span="24">
      <Input v-model="video.name" placeholder="视频名称"></Input>
    </Col>
  </Row>
  <Row class="rw">
    <Col span="5" class="lb">
      视频种类
    </Col>
    <Col span="19">
      <Select v-model="video.sort">
        <Option v-for="item in sorts" :value="item.id" :key="item.id">{{item.name}}</Option>
      </Select>
    </Col>
  </Row>
  <Row class="rw">
    <Col span="5" class="lb">
      上传视频
    </Col>
    <Col span="19">
      <Upload 
        ref="vdUploader" 
        action="/api/file/upload/video/" 
        name="file"
        :show-upload-list="true"
        :on-success="vdFinish">
        <Button type="ghost" icon="ios-cloud-upload-outline">上传视频</Button>
      </Upload>
    </Col>
  </Row>
  <Row class="rw">
    <Col span="5" class="lb">
      上传视频封面
    </Col>
    <Col span="19">
      <Upload 
        ref="cvUploader" 
        action="/api/file/upload/img/"
        name="file"
        :show-upload-list="true"
        :on-success="cvFinish">
        <Button type="ghost" icon="ios-cloud-upload-outline">上传文件</Button>
      </Upload>
    </Col>
  </Row>
  <Row class="rw">
    <Col span="24">
      <Input v-model="video.description" type="textarea" placeholder="视频简介"></Input>
    </Col>
  </Row>
</div>
</template>

<script>
export default{
  name:'VideoDialog',
  data(){
    return{
      video:{
        name:'',
        description:'',
        url:'',
        cover:'',
        sort:1
      },
      sorts:[]
    }
  },
  methods:{
    vdFinish(rsp,fi,list){
      let vm = this
      if(rsp.code==200){
        vm.$Notice.success({
          title:'视频上传成功',
          desc:'你有新的投稿'
        })
        vm.video.url = rsp.data
      }else vm.$Notice.error({
        title:'视频上传失败',
        desc:rsp.msg
      })
    },
    cvFinish(rsp,fi,list){
      let vm = this
      if(rsp.code==200){
        vm.$Notice.success({
          title:'封面上传成功',
          desc:'视频有封面啦！！！'
        })
        vm.video.cover = rsp.data
      }else vm.$Notice.error({
        title:'封面上传失败',
        desc:rsp.msg
      })
    },
    fetchSort(){
      let vm = this
      vm.$axios.get('/api/common/sort/').then(rsp=>{
        if(rsp.data.code==200) vm.sorts = rsp.data.data
          else console.log(rsp)
      }).catch(err=>{
        console.log(err)
      })
    }
  },
  mounted(){
    let vm = this
    vm.fetchSort()
  }
}
</script>

<style>
</style>
