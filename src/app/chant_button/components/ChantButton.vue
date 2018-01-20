<template>
	
	<div class="speak-button">
		<img :id="elementId" :class="{glow: glow}" @click="clicked()" src="static/images/speak.png" />
	</div>
			
</template>

<script>

	import EventBus from '../../event-bus'
	import Vue from 'vue';

	import VueLocalStorage from 'vue-localstorage'
	
	Vue.use(VueLocalStorage);
	
	export default {
	
		name: 'chant_button',
		
		data(){
		
			return {
			
				tipsoElement: false,
				elementId: 'chant-trigger-btn',
				timeOut: 3000,
				glow: false,
				timeObj: false,
			
			}
		
		},
		
		mounted(){
			
			var that = this;
			
			/*if button has not been clicked ever before, start 
			* highlighting it after a few seconds it so that it 
			* grabs user's attention
			*/
			
			if(!this.hasBeenClicked()){
			
				this.timeObj = setTimeout(function(){
				
									that.initTooltip();
				
								}, this.timeOut);
					
			}	
			
		},
		
		methods: {
		
			initTooltip(){
			
				this.tipsoElement = $("#"+this.elementId);
						
				this.tipsoElement.tipso({
				
					content: 'Click this button and speak- "Hare rama hare ram ram ram hare hare, hare krishna hare krishna krishna krishna hare hare"',
					width: 300,
					offsetX: -1,
					background: '#f74344',
					offsetY: 5,
					animationIn: 'bounceIn',
					animationOut: 'bounceOut',

				
				});
				
				this.glow = true;
				
				this.tipsoElement.tipso('show');	
				
			
			},
			
			distroyTooltip(){
			
				//disable the glowing effect
				this.glow = false;
				
				//destroys the tool-tip 
				if(this.tipsoElement){
				
					this.tipsoElement
						.tipso('hide')
						.tipso('destroy');
				
				}
			
				//keep track of this "click", store it in localStorage
				Vue.localStorage.set('clicked', true);
				
				//cancel the Timeout object, if any
				if(this.timeObj){
				
					clearTimeout(this.timeObj);
					
				}	
			
			},
  
			hasBeenClicked(){
			
				return Vue.localStorage.get('clicked', false)
			
			},	
  
			clicked(){
			
				/*gets triggered when the button is clicked for the very first time
				* keep track of this event 
				*/
				if(!this.hasBeenClicked()){
				
					this.distroyTooltip();
						
				}
			
				EventBus.$emit('trigger-mic');
							
			}
  
		},
		
	
	}

</script>