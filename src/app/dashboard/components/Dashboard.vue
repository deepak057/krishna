<template>
	
	<div class="container demo-1">
		
		
            <!--<nav class="codrops-demos">
				<a class="current-demo" href="index.html">Demo 1</a>
				<a href="index2.html">Demo 2</a>
			</nav>-->

            <div id="slider" class="sl-slider-wrapper">

				<div class="sl-slider">
				
					<div v-for="(item, index) in content" class="sl-slide"  :data-orientation="index % 2== 0? 'horizontal': 'vertical'" :data-slice1-rotation="getRandomInteger()" :data-slice2-rotation="getRandomInteger()" :data-slice1-scale="getRandomInteger(2)" :data-slice2-scale="getRandomInteger(2)" >
						<div class="sl-slide-inner">
								<div class="deco">
									<div class="circle">
										<img :class="['img-'+(index+1), 'content-image br']" :src="item.image"  />
										
									</div>
								
										
								</div>
								<h2>{{item.heading}}</h2>
								<blockquote><p>{{item.content}}</p><cite>{{item.muted}}</cite></blockquote>
						</div>
				</div>
				
					
				</div><!-- /sl-slider -->
				
				<nav id="nav-arrows" class="nav-arrows">
					<span class="nav-arrow-prev">Previous</span>
					<span class="nav-arrow-next">Next</span>
				</nav>

				<nav id="nav-dots" class="nav-dots">
					<span v-for="n in content.length" :class="{'nav-dot-current': (n==1)}"></span>
					
				</nav>

			</div><!-- /slider-wrapper -->

        </div>
	
</template>


<script>

	export default {
	
		name: 'dashboard',
		
		mounted(){
		
			  
		
		},
		
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
			
			getRandomInteger(number_){
			
				var num = Math.floor(Math.random()*(number_? number_: 25)) + 1; 
				num *= Math.floor(Math.random()*2) == 1 ? 1 : -1; 				
				return num;
			
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