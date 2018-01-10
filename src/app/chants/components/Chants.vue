<template>

	<bootstrap-modal centered  class="custom-popup" role="dialog" ref="theModal" :need-header="true" :need-footer="false">
			<div slot="title">
			</div>
			<div slot="body">
				<div class="text-center">
					<!-- <img src="static/images/mic.png" />-->
					
					<div :class="['circle-loader', {'success': success, error: speechError, 'load-complete': success || speechError } ]">
						<div v-show="success" class="checkmark draw"></div>
					</div>
					
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
	
	export default {
	
		components: {
		
			'bootstrap-modal': require('vue2-bootstrap-modal')
		
		},
	
		name: 'chants',
		
		
  data(){
  
	return {
	
				recognition: '',
				message: 'Listening...',
				chantsCount: 2,
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
				
				],
				
				images: [
				
					"http://www.hindugodwallpaper.com/images/gods/zoom/3196_shri-krishna-geeta-updesh.jpg",
					"https://i.pinimg.com/564x/a3/76/29/a37629535cae48f26e2e7d914d74b651.jpg",
					"http://wallpapers.iskcondesiretree.com/wp-content/wallpapers/artist/krishna_balaram/003-Sri_Sri_Krishna_Balaram.jpg",
				
				],
				
				content: [
				
				
					{
					
						heading: 'A BENE PLACITO',
						content: 'You have just dined, and however scrupulously the slaughterhouse is concealed in the graceful distance of miles, there is complicity.',
						muted: 'RALPH WALDO EMERSON',
						image: 'static/images/hqdefault.jpg',

					
					},
					
					{
					
						heading: 'Regula aurea',
						content: 'Until he extends the circle of his compassion to all living things, man will not himself find peace.',
						muted: 'ALBERT SCHWEITZER',
						image: 'static/images/slide 10 Arjuna and Krishna.jpg',
					
					},
					
					{
					
						heading: 'DUM SPIRO, SPERO',
						content: "Thousands of people who say they 'love' animals sit down once or twice a day to enjoy the flesh of creatures who have been utterly deprived of everything that could make their lives worth living and who endured the awful suffering and the terror of the abattoirs.",
						muted: 'DAME JANE MORRIS GOODALL',
						image: 'static/images/aec354cbe438e514c7ff271e84e49d3f--krishna-pictures-krishna-photos.jpg',

					},
					
					{
					
						heading: 'Supersoul is everywhere',
						content: "We are all pieces and parcels of Supreme Personality of Godhead",
						muted: 'LORD KRISHNA',
						image: 'static/images/003-Sri_Sri_Krishna_Balaram.jpg',
					
					
					},
					
					
					{
					
						heading: 'Supersoul is everywhere',
						content: "We are all pieces and parcels of Supreme Personality of Godhead",
						muted: 'LORD KRISHNA',
						image: 'static/images/9ed179ec62ee53d81eb9a4199a2fbe4d.jpg',
					
					
					},
					
					
				],
				
				currentImage: '',
	
	}
  
  },
  
  mounted(){
			
			var that = this;
			
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
	
	speechDetected(value_){
	
		if(this.mhaMantra.indexOf(value_)!=-1){
		
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
	
		this.chantsCount++;
		
		this.updateChants();
		
		this.preloaderSuccess();
		
		this.setValue("Hare Krishna, loading....");
		
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
		
		this.setValue("Not right, chant again.");
		
		this.closePopup(2000);
	
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