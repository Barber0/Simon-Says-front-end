<template>
<div>
  <div id="player"></div>
</div>
</template>

<script>
import 'dplayer/dist/dplayer.min.css'
import dplayer from 'dplayer'
export default{
  name:'VdPanel',
  props:['video','user'],
  data(){
    return{
      dp:{},
      danmaku:[{}]
    }
  },
  methods:{
    initVd(){
      let vm = this
      vm.dp = new dplayer({
        container: document.getElementById('player'),
        screenshot:true,
        video:{
          url: vm.video.url,
          pic: vm.video.cover,
          thumbnails: vm.video.cover
        },
        danmaku:{
          id: vm.video.id,
          api: '/api/danmaku/',
          user: vm.user.id,
        }
      })
      vm.dp.on('canplay',function(){vm.$parent.danRow = vm.dp.danmaku.dan})
    }
  },
  mounted(){
    let vm = this
    setTimeout(() => {
      vm.initVd()
    }, 500);
  }
}
</script>