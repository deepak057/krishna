<template>

	<div class="container demo-1">
		
            <!--<nav class="codrops-demos">
				<a class="current-demo" href="index.html">Demo 1</a>
				<a href="index2.html">Demo 2</a>
			</nav>-->

            <div id="slider" class="sl-slider-wrapper">

				<div class="sl-slider">
				
					<div v-for="(item, index) in sliderContent" class="sl-slide"  :data-orientation="index % 2== 0? 'horizontal': 'vertical'" :data-slice1-rotation="getRandomInteger()" :data-slice2-rotation="getRandomInteger()" :data-slice1-scale="getRandomInteger(2)" :data-slice2-scale="getRandomInteger(2)" >
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
					<span v-for="n in slideIndex" :key="n" @click="dotClicked(n)" :class="{'nav-dot-current': (n==1)}"></span>
					
				</nav>

			</div><!-- /slider-wrapper -->

        </div>
	

</template>

<script>
	
	import EventBus from '../../event-bus';

	const slider =  {
	
		name: 'slider',
		
		mounted(){
		
			var that = this;
			
			this.getNewSlideContent();
			
			window.onload = function(){
			
				that.initSlider();
			}
			
			EventBus.$on("push-new-slide", function(){
			
				that.pushNewSlide();			
			
			});
			
		},
		
		data(){
		
			return {
			
				
				slitslider: {},
				page: {},
				slideIndex: 1,
				
				
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
				
				copy: [],
				sliderContent: [],
				flag: false,
							
			}
		
		},
		
		methods: {
		
			getRandomInteger(number_){
			
				var num = Math.floor(Math.random()*(number_? number_: 25)) + 1; 
				num *= Math.floor(Math.random()*2) == 1 ? 1 : -1; 				
				return num;
			
			},
			
			copyContent(){
				this.copy = this.content.slice();
			},
			
			getNewSlideContent() {
								  
				if (this.copy.length < 1) { 
					this.copyContent();
				}
				var index = Math.floor(Math.random() * this.copy.length);
				var item = this.copy[index];
				this.copy.splice(index, 1);	
				
				if(!this.flag){
					this.sliderContent.push(item);
					this.flag = true;
				}
				
				return item;			  
			},
			
			
			initSliderEvent(){
			

				// add navigation events
				$navArrows.children( ':last' ).on( 'click', function() {

					that.slitslider.next();
					
					return false;
							

				} );	
			
			},
			
			initSlider(){
			
				var that = this,
				$navArrows = $( '#nav-arrows' );
				
					
				this.slitslider = $( '#slider' ).slitslider( {
							onBeforeChange : function( slide, pos ) { 
							
								
							},
							
							onAfterChange: function(slide, pos){
								
								var $nav = that.getNav();

								$nav.removeClass( 'nav-dot-current' );
								$nav.eq( pos ).addClass( 'nav-dot-current' );

								
								that.applySlideColor(pos)	
							
							},
							
						} );
						
						
						
				// add navigation events
				$navArrows.children( ':last' ).on( 'click', function() {

					that.slitslider.next();
					
					return false;
					
			
				});
				
				$navArrows.children( ':first' ).on( 'click', function() {
								
					that.slitslider.previous();
					return false;

				});
				
				this.applySlideColor(1);
				
			},
			
			getNav(){
			
				return $( '#nav-dots > span' );
			
			},
			
			dotClicked($index){
				
				var $nav = this.getNav();
				
				if( !this.slitslider.isActive() ) {

					$nav.removeClass( 'nav-dot-current' );
					$nav.eq($index-1).addClass( 'nav-dot-current ');
						
				}
						
						
				this.slitslider.jump( $index );
							
			},
			
			applySlideColor(pos){
				
					$( ".content-image").removeAttr("data-adaptive-background");

					var img = $(".img-"+(pos));
					
					if(!img.parents(".sl-slide-inner:first").hasClass("color-added")){
					
						img.attr("data-adaptive-background", "");
						
						
					/*var blob = new Blob([
					"onmessage = function(e) { var data = e.data; alert(data.e);  postMessage('msg from worker');}"]);

					// Obtain a blob URL reference to our worker 'file'.
					var blobURL = window.URL.createObjectURL(blob);

					var worker = new Worker(blobURL);
					worker.onmessage = function(e) {
					  alert(e.data);
					};
					
					var e=document.createElement('canvas');
					worker.postMessage({e:e}); // Start the worker.
									
						return ;
						
						*/
						
						
						/*var colorThief = new ColorThief();
						var color= colorThief.getColor(img[0]);
						
						img.parents(".sl-slide-inner:first").css({
									
							background: "rgb("+color+")",
									
						});*/
							
						
						
						return;
						
						RGBaster.colors(img[0], {
						success: function(payload) {
							
							img.parents(".sl-slide-inner:first").css({
									
										background: payload.dominant,
									
									});
							
							// You now have the payload.
							console.log(payload.dominant);
							console.log(payload.secondary);
							console.log(payload.palette);
							}
						});
						
						
						 return;
						
						
						
						
						
						$.adaptiveBackground.run({
							
								success($img, data) {
								
									alert(data.color);
									
									$img.parents(".sl-slide-inner:first").css({
									
										background: data.color,
									
									}).addClass("color-added");
									
								
								}
	
							
						});
					}	
				
			},

			
			addNewSlide(obj){
				
				var that = this;
				
				var items = $('<div class="sl-slide"  data-orientation="'+ (that.slideIndex%2==0? "horizontal": "vertical") +'" data-slice1-rotation="'+that.getRandomInteger()+'" data-slice2-rotation="'+that.getRandomInteger()+'" data-slice1-scale="'+that.getRandomInteger(2)+'" data-slice2-scale="'+that.getRandomInteger(2)+'" ><div class="sl-slide-inner"><div class="deco"><div class="circle"><img class="img-'+that.slideIndex+' content-image br" src="'+obj.image+'"  /></div></div><h2>'+obj.heading+'</h2><blockquote><p>'+obj.content+'</p><cite>'+obj.muted+'</cite></blockquote></div></div>');
				
				that.slitslider.add(items);
				
				var img = $(".img-"+(that.slideIndex));
				
				
				RGBaster.colors(img[0], {
						success: function(payload) {
							
							img.parents(".sl-slide-inner:first").css({
									
										background: payload.dominant,
										
									
									});
							
							
							that.slitslider.jump(that.slideIndex);

							
							// You now have the payload.
							console.log(payload.dominant);
							console.log(payload.secondary);
							console.log(payload.palette);
							}
						});
				
				
				
												
				that.slideIndex++;
				
						
			
	
			},	
			
			pushNewSlide(){
					
					var obj = this.getNewSlideContent();
										
					this.addNewSlide(obj);
			
			},
			
		
		},
		
		
	}
	
	export default slider;

</script>