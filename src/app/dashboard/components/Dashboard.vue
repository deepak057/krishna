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
			
			<chant_button></chant_button>		
			<slider></slider>
			<chants></chants>
		
		</div>
	</div>	
	
</template>


<script>
	
	import EventBus from '../../event-bus';
	import { Slider } from '../../slider/components';
	import { Chants } from '../../chants/components';
	import { ChantButton } from '../../chant_button/components';

	
	export default {
	
		components: {
			Slider,
			Chants,
			"chant_button": ChantButton
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
		
  	
	}

</script>