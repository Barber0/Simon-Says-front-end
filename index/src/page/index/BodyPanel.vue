<template>
<div>
  <div class="ltpn">
    <VideoList :list="videos" />
    <div class="pagi">
      <Page :current="pagi.page" :total="pagi.total" :page-size="pagi.size" @on-change="$parent.changePage" />
    </div>
  </div>
  <div class="rtpn">
    <Affix :offset-top="100">
      <div class="tl">
        <Icon type="navicon-round" size="35"></Icon>
        <span>排行</span>
      </div>
      <RankList ref="ranklist" />
    </Affix>
  </div>
</div>
</template>

<script>
import RankList from './RankList'
import VideoList from './VideoList'
export default{
  name:'body-panel',
  props:['videos','pagi','rank'],
  data(){
    return{
    }
  },
  components:{
    VideoList,
    RankList
  }
}
</script>

<style>

</style>
