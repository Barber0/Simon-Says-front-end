<template>
<Card class="rtpn">
  <div v-for="(item, index) in list" :key="index" class="rk-row">
    <a :href="'/video/#/'+item.id">
      <Icon style="float:left;" type="navigate"></Icon>
      <span class="title one-line">{{item.name}}</span>
      <span class="heat">{{item.view}}</span>
    </a>
  </div>
</Card>
</template>

<script>
export default{
  name:'RankList',
  data(){
    return{
      list:[{}]
    }
  },
}
</script>

<style>

</style>
