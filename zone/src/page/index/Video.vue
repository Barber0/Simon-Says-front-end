<template>
<div class="vd hf">
  <a :href="info.link" target="blank">
    <img :src="info.cover">
    <div class="one-line txt" v-text="info.name"></div>
    <div class="dtl">
      <div class="one-line txt upper" v-text="info.upper"></div>
      <div class="one-line txt created_at" v-text="createAt"></div>
    </div>
  </a>
</div>
</template>

<script>
export default{
  name:'Video',
  props:['info'],
  computed:{
    createAt(){
      let vm = this
      return vm.dateToString(new Date(vm.info.createAt))
    }
  },
  methods:{
    dateToString(date){ 
      let year = date.getFullYear(); 
      let month =(date.getMonth() + 1).toString(); 
      let day = (date.getDate()).toString();  
      if (month.length == 1) { 
          month = "0" + month; 
      } 
      if (day.length == 1) { 
          day = "0" + day; 
      }
      let dateTime = year + "-" + month + "-" + day;
      return dateTime; 
    }
  }
}
</script>

<style>

</style>
