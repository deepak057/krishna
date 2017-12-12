<template>

	<div class="panel">
	
		<div class="panel-body">
			
			<div class="example-box-wrapper">
			
				<div class="row">
				
					<div class="col-md-6">
					
						<button @click="click" class="btn btn-lg btn-danger " data-style="light" data-theme="bg-black" data-opacity="60">Chant Now</button>
		
						<div class="text-danger">
			
							{{message}}
						
						</div>
					
						
						<h2 class="mt-5 mrg10T">You Chanted: <span class="text-success">{{chantsCount}}</span></h2>
					
						<ul class="text-success mrg5T todo-box" v-html="chants">
						
							
						</ul>
					
					
					</div>
					
					
					<div class="col-md-6">
					
						<img :src="currentImage" style="height:300px" />
					
					</div>
				
				
				</div>
				
			
			</div>
			
	
		</div>
		
	</div>

</template>


<script>

	export default {
	
		name: 'dashboard',
		
		data(){
		
			return {
			
				
				recognition: '',
				message: 'Default message',
				chantsCount: 2,
				chants: "",
				mhaMantra: [
				
					"Hare Ram Hare Ram Ram Ram Hare Hare Hare Krishna Hare Krishna Krishna Krishna Hare Hare",
					"Hare Rama Hare Rama Rama Rama Hare Hare Hare Krishna Hare Krishna Krishna Krishna Hare Hare",

				
				],
				
				messages: [
				
					"Sorry, You need to use Chrome to be able to use this feature",
					'Voice recognition activated. Try speaking into the microphone.',
					'You were quiet for a while so voice recognition turned itself off.',
					'No speech was detected. Try again.',
				
				],
				
				images: [
				
					"http://www.hindugodwallpaper.com/images/gods/zoom/3196_shri-krishna-geeta-updesh.jpg",
					"https://i.pinimg.com/564x/a3/76/29/a37629535cae48f26e2e7d914d74b651.jpg",
					"http://wallpapers.iskcondesiretree.com/wp-content/wallpapers/artist/krishna_balaram/003-Sri_Sri_Krishna_Balaram.jpg",
				
				],
				
				currentImage: '',
			
			}
		
		},
		
		mounted(){
		
			this.afterUpdate();
		
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
							  par.setValue(transcript)
							}

				}
				
				this.recognition.onspeechend = function() {
				  par.setValue(par.messages[2]);
				  par.recognition.start();
				}

				this.recognition.onerror = function(event) {
				  if(event.error == 'no-speech') {
					par.setValue(par.messages[3]);  
				  };
				}
		},
		
		methods: {
	
			click(){
				
				//this.recognition.start();
				this.setValue(this.mhaMantra[0]);
				
			},
			
			setValue(value_){
			
				if(this.mhaMantra.indexOf(value_)!=-1){
				
					this.chantsCount++;
									
				}
				
				else {
				
					this.message = value_;
				
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
			
			
			updateImage(){
			
				this.currentImage = this.images[Math.floor(Math.random() * this.images.length)];
			
			},
		
			afterUpdate(){
			
				this.updateChants();
				
				this.updateImage();
			
			}
		
		},
		
		watch: {
		
			chantsCount(newv, oldv){
			
				this.afterUpdate();
			
			},
		
		}
	
	}

</script>