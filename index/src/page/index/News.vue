<template>
<div class="news">
  <a target="blank" :href="link">
    <img :src="info.cover">
    <div class="news-tl">{{info.name}}</div>
  </a>
</div>
</template>

<script>
export default{
  props:['info'],
  name:'news',
  data(){
    return{
    }
  },
  computed:{
    link(){
      let vm = this
      return '/video/#/'+vm.info.id
    }
  }
}
</script>

<style>

</style>
