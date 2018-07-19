<template>
<div>
  <Carousel autoplay v-model="value1" class="gallery" loop>
		<CarouselItem>
			<div class="item">
				<img src="/static/banner1.jpg">
			</div>
		</CarouselItem>
		<CarouselItem>
			<div class="item">
				<img src="/static/banner2_1.png">
			</div>
		</CarouselItem>
		<CarouselItem>
			<div class="item">
				<img src="/static/banner2_2.png">
			</div>
		</CarouselItem>
	</Carousel>
</div>
</template>

<script>
export default{
	name:'gallery',
	data(){
		return{
			value1:0,
		}
	}
}    
</script>

<style>

</style>
