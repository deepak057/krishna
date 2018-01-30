<template>

	<bootstrap-modal centered  class="custom-popup" role="dialog" ref="theModal" :need-header="true" :need-footer="false">
			<div slot="title">
			</div>
			<div slot="body">
				<div class="text-center">
					<!-- <img src="static/images/mic.png" />-->
					
					<div v-show="!speechError" :class="['circle-loader', {'success': success, error: speechError, 'load-complete': success || speechError } ]">
						<div v-show="success" class="checkmark draw"></div>
					</div>
					
					<svg  v-show="speechError" version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 130.2 130.2">
					  <circle class="path circle" fill="none" stroke="#d9534f" stroke-width="2" stroke-miterlimit="10" cx="65.1" cy="65.1" r="62.1"/>
					  <line class="path line" fill="none" stroke="#d9534f" stroke-width="2" stroke-linecap="round" stroke-miterlimit="10" x1="34.4" y1="37.9" x2="95.8" y2="92.3"/>
					  <line class="path line" fill="none" stroke="#d9534f" stroke-width="2" stroke-linecap="round" stroke-miterlimit="10" x1="95.8" y1="38" x2="34.4" y2="92.2"/>
					</svg>
					
					<h1 :class="{'blink-text': success}">{{message}}</h1>
					
					<div v-show="!success && !speechError">
						<p v-show="chantsCount" class="chants-meta">You have chanted <a :title="!showChants? 'Show Chants': 'Hide Chants'"  @click="showChants= !showChants" hrfe="#" class="pointer hover-underline">{{chantsCount}}</a> times</p>
						<p v-show="showChants" v-html="chants" class="chants-container text-success text-center"></p>
					
					</div>
					
				</div>
			</div>
		</bootstrap-modal> 
	

</template>


<script>
	
	import EventBus from '../../event-bus';
	import Vue from 'vue';
	import VueLocalStorage from 'vue-localstorage'
	
	Vue.use(VueLocalStorage);
	
	export default {
	
		components: {
		
			'bootstrap-modal': require('vue2-bootstrap-modal')
		
		},
	
		name: 'chants',
		
		
  data(){
  
	return {
	
				recognition: '',
				message: 'Listening...',
				chantsCount: parseInt(Vue.localStorage.get("chantsCount", 0)),
				chants: "",
				showChants: false,
				success: false,
				speechError: false,
				
				mhaMantra: [
				
					"Hare Ram Hare Ram Ram Ram Hare Hare Hare Krishna Hare Krishna Krishna Krishna Hare Hare",
					"Hare Rama Hare Rama Rama Rama Hare Hare Hare Krishna Hare Krishna Krishna Krishna Hare Hare",
					"hey",
					"1",
					"change",
				
				],
				
				messages: [
				
					"Sorry, You need to use Chrome to be able to use this feature",
					'Voice recognition activated. Try speaking into the microphone.',
					'You were quiet for a while, so voice recognition turned itself off.',
					'No speech was detected. Try again.',
					"Hare Krishna, loading....",
					"Not right, chant again.",
					
				
				],
				
				currentImage: '',
	
	}
  
  },
  
  watch: {
  
	chantsCount(new_v, old_v){
	
		Vue.localStorage.set("chantsCount", new_v);
	
	},
  
  },
  
  mounted(){
			
			var that = this;

			$(this.$refs.theModal).on("hidden.bs.modal", this.afterModalClosed);
			
			EventBus.$on('trigger-mic',function(){
			
				that.trigger();
			
			});
			
			
			EventBus.$on('close-mic-popup', function(){
			
				that.closePopup();
			
			});
				
			var par = this;
					
			try {
				  var SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
				  this.recognition = new SpeechRecognition();
				}
				catch(e) {
				  console.error(e);
				  par.setValue(par.messages[0]);
				}
				
				this.recognition.onstart = function() { 
					par.setValue(par.messages[1]);
				}
				
				this.recognition.onresult = function(event) {

					  var current = event.resultIndex;

					  var transcript = event.results[current][0].transcript;
					  
					  var mobileRepeatBug = (current == 1 && transcript == event.results[0][0].transcript);

							if(!mobileRepeatBug) {
							
							  par.speechDetected(transcript)
							
							
							}

				}
				
				this.recognition.onspeechend = function() {
				  //par.setValue(par.messages[2]);
				  //par.recognition.start();
				}

				this.recognition.onerror = function(event) {
				  if(event.error == 'no-speech') {
					
					par.setValue(par.messages[3]); 
					
					par.closePopup(2000);
					
				  }
				  
				}
		},
		
  
  methods: {
	trigger(){
		
			var that = this;
			
			/*reset these bools */	
			this.success = false;
			this.speechError = false;
		
		  this.$refs.theModal.open();
		  this.recognition.start();
		  
		  /*setTimeout(function(){
		  
			//that.setValue(that.mhaMantra[0]);
			that.speechSuccess();
			//that.speechFailed();

		  
		  }, 2000);*/
		  
	
	},
	
	countOccurrences(string, subString, allowOverlapping) {

		string += "";
		subString += "";
		if (subString.length <= 0) return (string.length + 1);

		var n = 0,
			pos = 0,
			step = allowOverlapping ? 1 : subString.length;

		while (true) {
			pos = string.indexOf(subString, pos);
			if (pos >= 0) {
				++n;
				pos += step;
			} else break;
		}
		return n;
	},
	
	getChantsCount(speech_text){
	
		var count = 0;
	
		for (var i in this.mhaMantra){
		
			count += this.countOccurrences(speech_text, this.mhaMantra[i]);
		
		}
		
		return count;
	
	},
	
	speechDetected(value_){
	
		var chantsCount = this.getChantsCount(value_);
		
		if(chantsCount){
			
			this.chantsCount+= chantsCount;
			
			this.speechSuccess();				
		}
		
		else {
					
			this.speechFailed();
		
		}
	
	},
	
	setValue(value_){
			
			this.message = value_;
			
	},
	
	
	speechSuccess(){
			
		this.updateChants();
		
		this.preloaderSuccess();
		
		this.setValue(this.messages[4]);
		
		setTimeout(function(){
			
			EventBus.$emit("push-new-slide");

		
		}, 500);
		
		
	},

	preloaderSuccess(){
	
		this.success = true;
	
	},
	
	preloaderError(){
	
		this.speechError = true;
	},
	
	speechFailed(){
	
		this.preloaderError();
		
		this.setValue(this.messages[5]);
		
		this.closePopup(2000);
	
	},
	
	afterModalClosed(){alert("here");
	
		/*
		** Stop the speech recognition engine if the popup 
		** is closed
		*/
		if(this.recognition){
		
			this.recognition.stop();
		
		}
	
	},
	
	closePopup(timeout_){
	
		if(timeout_){
			
			var that = this;
			
			setTimeout(function(){
			
				that.$refs.theModal.close();
			
			}, timeout_);
		
		}
		
		else {
		
			this.$refs.theModal.close();
		}
	},
	
	updateChants(){
	
		if(this.chantsCount){
		
			this.chants = "";
		
			for( var i=1; i<=this.chantsCount; i++){
			
				this.chants += '&#10003; '+this.mhaMantra[0]+'<br/>';
			
			}
			
			return this.chants;
		
		}
	
	},
	
	
  },
  
  
}

	
</script>