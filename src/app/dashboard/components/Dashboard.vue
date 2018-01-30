<template>
	
	<div>
		<page_loader v-show="!pageLoaded"></page_loader>
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
	import { PageLoader } from '../../page_loader/components';


	
	export default {
	
		components: {
			Slider,
			Chants,
			"chant_button": ChantButton,
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