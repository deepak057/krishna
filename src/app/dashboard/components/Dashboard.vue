<template>
	
	<div>
		<div class="speak-button">
				<img @click="clicked()" src="static/images/speak.png" />
			</div>
				
		<slider></slider>
		<chants></chants>
		</div>
	
</template>


<script>

	import { Slider } from '../../slider/components';
	import { Chants } from '../../chants/components';
	import EventBus from '../../event-bus';

	export default {
	
		components: {
			Slider,
			Chants
		},
	
		name: 'dashboard',
		methods: {
  
			clicked(){
			
				EventBus.$emit('trigger-mic');
							
			}
  
		}
  	
	}

</script>