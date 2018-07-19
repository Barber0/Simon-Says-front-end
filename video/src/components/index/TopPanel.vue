<template>
<div>
<div class="ltpn">
  <div class="vdtl"><h1 v-text="video[0].name" class="one-line"></h1></div>
  <div>
    <Row class="rw">
      <Col span="4">
        <Icon type="person"></Icon>
        <b><span v-text="video[0].upper"></span></b>
      </Col>
      <Col span="4">
        <Icon type="play" size="16"></Icon>
        <b>
          <span v-text="video[0].view"></span>
          <span>次</span>
        </b>
      </Col>
      <Col span="4">
        <Icon type="clock" size="16"></Icon>
        <span v-text="date"></span>
      </Col>
      <Col span="4">
        <Icon type="document-text"></Icon>
        <span v-text="video[0].sort"></span>
      </Col>
    </Row>
  </div>
</div>
<div class="rtpn">
  <Row>
    <Col span="7">
      <img :src="video[1].header">
    </Col>
    <Col span="17">
      <div class="nknm"><h2 v-text="video[1].nickname"></h2></div>
      <div v-text="video[1].intro"></div>
    </Col>
  </Row>
  <!-- <div v-text="video[1]"></div> -->
</div>
</div>
</template>

<script>
import Utils from '@/components/utils'
export default{
  name:'TopPanel',
  props:['video'],
  data(){
    return{
      upper:{}
    }
  },
  computed:{
    date(){
      let vm = this
      return Utils.dateToStr(new Date(vm.video[0].createAt))
    }
  },
  methods:{
  },
  mounted(){
  }
}
</script>