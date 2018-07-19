<template>
<div>
<Card class="vd-list">
  <Row style="min-height:300px;">
    <div>
      <div v-for="(item, index) in vdList" :key="index" class="vd-wrapper">
        <Video :info="item" />
        <div class="vd-ope">
          <Button type="primary" @click="openVdEdit(item)">修改</Button>
          <Button type="ghost" @click="dltVd(item)">删除</Button>
        </div>
      </div>
    </div>
  </Row>
  <Row>
    <div class="pagi">
      <Page :current="pagi.page" :total="pagi.total" :page-size="pagi.size" @on-change="changePage" />
    </div>
  </Row>
</Card>
<Modal
  v-model="editDialog"
  title="视频信息编辑"
  @on-ok="updateVd">
  <div class="dialog">
    <Row class="rw">
      <Col span="3" class="lb">
        视频名称
      </Col>
      <Col span="12">
        <Input v-model="editVd.name" placeholder="视频名称"></Input>
      </Col>
    </Row>
    <Row class="rw">
      <Col span="3" class="lb">
        板块
      </Col>
      <Col span="12">
        <Select v-model="editVd.sort">
          <Option v-for="item in sorts" :value="item.id" :key="item.id" v-text="item.name"></Option>
        </Select>
      </Col>
    </Row>
    <Row class="rw">
      <Col span="24">
        <Input v-model="editVd.description" type="textarea" placeholder="视频描述"></Input>
      </Col>
    </Row>
  </div>
</Modal>
</div>
</template>

<script>
import Video from '@/page/index/Video'
export default{
  name:'VideoList',
  props:['user'],
  data(){
    return{
      vdList:[],
      editDialog:false,
      editVd:{
        id:'',
        name:'',
        description:'',
        sort:1
      },
      sorts:[],
      pagi:{
        total:0,
        page:1,
        size:15
      }
    }
  },
  methods:{
    fetchVideos(){
      let vm = this
      vm.$axios.get('/api/file/vdpage/?page='+vm.pagi.page+"&size="+vm.pagi.size).then(rsp=>{
        if(rsp.data.code==200) {
          vm.vdList = rsp.data.data.content
          for(let i=0;i<vm.vdList.length;i++) vm.vdList[i].link = '/video/#/'+vm.vdList[i].id
          vm.pagi.total = rsp.data.data.totalElements
        }else console.log(rsp)
      }).catch(err=>{
        console.log(err)
      })
    },
    openVdEdit(vd){
      let vm = this
      // vm.editVd = vd
      vm.editVd.id = vd.id
      vm.editVd.name = vd.name
      vm.editDialog = true
    },
    fetchSorts(){
      let vm = this
      vm.$axios.get('/api/common/sort/').then(rsp=>{
        if(rsp.data.code==200) vm.sorts = rsp.data.data
          else console.log(rsp)
      }).catch(err=>{
        console.log(err)
      })
    },
    updateVd(){
      let vm = this
      vm.$axios.put('/api/file/video/',vm.editVd).then(rsp=>{
        if(rsp.data.code==200){
          vm.$Notice.success({
            title:'编辑成功',
            desc:'成功修改视频信息'
          })
          vm.fetchVideos()
        }else vm.$Notice.error({
          title:'编辑失败',
          desc:rsp.data.msg
        })
      }).catch(err=>{
        console.log(err)
      })
    },
    deleteVd(id){
      let vm = this
      vm.$axios.delete('/api/file/video/?id='+id).then(rsp=>{
        console.log(rsp)
        if(rsp.data.code==200){
          vm.fetchVideos()
          vm.$Notice.success({
            title:'删除成功',
            desc:'成功删除了视频（id:'+id+'）'
          })
        }else vm.$Notice.error({
          title:'删除失败',
          desc:rsp.msg
        })
      })
    },
    dltVd(item){
      let vm = this
      if(confirm("是否确定要删除此视频")){
        vm.deleteVd(item.id)
      }
    },
    changePage(pg){
      let vm = this
      vm.pagi.page = pg
      vm.fetchVideos()
    }
  },
  components:{
    Video
  },
  mounted(){
    let vm = this
    vm.fetchVideos()
    vm.fetchSorts()
  }
}
</script>

<style>

</style>