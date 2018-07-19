<template>
<div class="video">
  <a target="blank" :href="link">
    <img :src="info.cover">
    <div class="info">
      <div class="vdtl">{{info.name}}</div>
      <div class="in">
        <div class="col">
          <Icon type="person" size="10"></Icon>
          <span v-text="info.upper"></span>
        </div>
        <div class="col" style="text-align:right" v-text="date"></div>
      </div>
    </div>
  </a>
</div>
</template>

<script>
import Utils from '@/components/utils'
export default{
  props:['info'],
  name:'Video',
  computed:{
    link(){
      let vm = this
      return "/video/#/"+vm.info.id
    },
    date(){
      let vm = this
      return Utils.dateToStr(new Date(vm.info.createAt))
    }
  },
  mounted(){
    let vm = this
    console.log(vm.info)
  }
}
</script>

<style>

</style>
