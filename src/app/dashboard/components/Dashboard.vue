<template>
	
	<div>
		
		<div class="loader" v-show="!pageLoaded">
		  <div class="side"></div>
		  <div class="side"></div>
		  <div class="side"></div>
		  <div class="side"></div>
		  <div class="side"></div>
		  <div class="side"></div>
		  <div class="side"></div>
		  <div class="side"></div>		
		</div>
		
		<div v-if="pageLoaded">
			<div class="speak-button">
				<img @click="clicked()" src="static/images/speak.png" />
			</div>
					
			<slider></slider>
			<chants></chants>
		
		</div>
	</div>	
	
</template>


<script>
	
	import EventBus from '../../event-bus';
	import { Slider } from '../../slider/components';
	import { Chants } from '../../chants/components';
	
	export default {
	
		components: {
			Slider,
			Chants
		},
		
		data(){
		
			return{
			
				pageLoaded: false,
			}
		},
		
		mounted(){
		
			var that = this;
						
			window.onload= function(){
						
				that.pageLoaded = true;
										
			};	
		
		},
	
		watch: {
		
			pageLoaded(new_, old){
					
				setTimeout(function(){
				
					EventBus.$emit("init-slider");

	
				}, 1);

			}
		
		},
	
		name: 'dashboard',
		methods: {
  
			clicked(){
			
				EventBus.$emit('trigger-mic');
							
			}
  
		}
  	
	}

</script>