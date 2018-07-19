<template>
<div class="vd-list">
  <div class="tl">
    <Icon type="ionic" size="35"></Icon>
    <span>视频</span>
  </div>
  <Video v-for="(item, index) in list" :key="index" :info="item" />
</div>
</template>

<script>
import Video from './Video'
export default{
  props:['list'],
  name:'VideoList',
  components:{
    Video
  }
}
</script>

<style>

</style>
