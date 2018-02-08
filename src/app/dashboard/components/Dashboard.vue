<template>
	
	<div>
		<page_loader v-show="!pageLoaded"></page_loader>
		<div v-if="pageLoaded">	
			<navigation></navigation>		
			<slider></slider>
			<chants></chants>
		</div>
	</div>	
	
</template>


<script>
	
	import EventBus from '../../event-bus';
	import { Slider } from '../../slider/components';
	import { Chants } from '../../chants/components';
	import { PageLoader } from '../../page_loader/components';
	import { Navigation } from '../../navigation/components';

	
	export default {
	
		components: {
			Slider,
			Navigation,
			Chants,
			"page_loader": PageLoader,
		},
		
		data(){
		
			return{
			
				pageLoaded: false,
			}
		},
		
		mounted(){
		
			var that = this;
				
			window.onload= function(){
				
				that.showPage();	
				
				setTimeout(function(){
				
					EventBus.$emit("init-slider");
						
				}, 1);
										
			};
		
		},
		
		methods: {
		
			showPage(){
			
				this.pageLoaded = true;
			
			}
		
		},
	
	
		name: 'dashboard',
		
  	
	}

</script>