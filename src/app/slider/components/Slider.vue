<template>
	
	<div>
	
		<page_loader v-show="!showSlider"></page_loader>

		<div class="container demo-1" v-if="showSlider">
		
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
										<img :class="['img-'+(index+1), 'content-image br']" :src="item.image.src"  />
										
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
	
		<gallary></gallary>
	
	</div>


</template>

<script>
	
	import EventBus from '../../event-bus';
	import { PageLoader } from '../../page_loader/components';
	import { Gallary } from '../../gallary/components';



	const slider =  {
	
		name: 'slider',
		
		components: {
		
			"page_loader": PageLoader,
			Gallary,
		
		},
		
		mounted(){
		
			var that = this;
			
			this.firstSlideContent = this.getNewSlideContent();
			
			EventBus.$on("push-new-slide", function(){
			
				that.pushNewSlide();			
			
			});
			
			EventBus.$on("init-slider", function(){
											
				that.initSlider();					
				
			});
			
			
			$(document).on("click", ".content-image", function(){
			
				var index_= $(".content-image").index(this);
			
				EventBus.$emit("jump-to-gallary-item", index_);
			
			})
			
		},
		
		data(){
		
			return {
			
				
				slitslider: {},
				page: {},
				slideIndex: 1,
				firstSlideContent: false,
				showSlider: false,
				
				content: [
				
				
					{
					
						heading: 'Live your own path',
						content: 'Far better to live your own path imperfectly than to live another’s perfectly.',
						muted: 'Krishna',
						image: {
					
							src: 'static/images/hqdefault.jpg',
							h: 360,
							w: 480,
						
						},
						
						

					
					},
					
					{
					
						heading: "Don't abandon duties...",
						content: '..because you see defects in them. Every action, every activity, is surrounded by defects as a fire is surrounded by smoke.',
						muted: 'Krishna',
						image: {
						
							src: 'static/images/slide 10 Arjuna and Krishna.jpg',
							w: 1024,
							h: 768,		
						
						},
						
						
					
					},
					
					{
					
						heading: "Whatever happened was good..",
						content: "what's happening, it's going well, whatever will happen, will also be good.",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/aec354cbe438e514c7ff271e84e49d3f--krishna-pictures-krishna-photos.jpg',
							w: 736,
							h: 588,
						
						},

					},
					
					{
					
						heading: "Reshape yourself through ..",
						content: "the power of your will. Those who have conquered themselves…live in peace, alike in cold and heat, pleasure and pain, praise and blame…",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/Lord-Hayagriva-The-Lesser-Known-Incarnation-of-Mahavishnu-2.jpg',
							w: 500,
							h: 616,
						
						},

					},
					
					{
					
						heading: "Abandon all attachment to the..",
						content: "results of action and attain supreme peace. When a person is devoted to something with complete faith, I unify his faith in that.",
						muted: 'Krishna',
						image: {
						
						
							src: 'static/images/krishna-images-17.jpg',
							w: 564,
							h: 752,
						
						},

					},
					
					{
					
						heading: "No one who does good work will..",
						content: " ever come to a bad end, either here or in the world to come.",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/lord-krishna-110a.jpg',
							w: 1024,
							h: 768,
						
						},

					},
					
					{
					
						heading: "It is Nature that causes all ..",
						content: 'movement. Deluded by the ego, the fool harbors the perception that says "I did it".',
						muted: 'Krishna',
						image: {
						
							src: 'static/images/gita-109.jpg',
							w: 600,
							h: 446,
						
						},

					},
					
					{
					
						heading: "Man is made by his belief.",
						content: "As he believes, so he is. You can be anything that you want to be.",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/gita-100.jpg',
							w: 600,
							h: 812,
						
						},

					},
					
					{
					
						heading: "For the one who has conquered..",
						content: "the mind..the mind is the best of friends. But for one who has failed to do so his very mind will be his greatest enemy",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/gita-110.jpg',
							w: 600,
							h: 395,
						
						},

					},
					
					{
					
						heading: "Lust, anger, and greed..",
						content: " are three gates to this self-destructive hell. Pleasures of the senses give birth to misery.",
						muted: 'Krishna',
						image: {
							
							src: 'static/images/gita-112.jpg',
							w: 600,
							h: 807,
						
						},

					},
					
					{
					
						heading: "Even if you were the most sinful...",
						content: "of sinners you could cross beyond all sin by the raft of spiritual wisdom.",
						muted: 'Krishna',
						image: {
							
							src: 'static/images/gita-136.jpg',
							w: 600,
							h: 812,
						
						},

					},
					
					
					{
					
						heading: "We are kept from our goal..",
						content: "not by obstacles, but by a clear path to a lesser goal.",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/gita-126.jpg',
							w: 600,
							h: 798,
						
						},

					},
					
		
					{
					
						heading: "Strive to still your thoughts..",
						content: "The mind is restless and difficult to restrain, but it is subdued by practice.",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/003-Sri_Sri_Krishna_Balaram.jpg',
							w: 800,
							h: 600,
						
						}

					},
					
					{
					
						heading: "One has to learn tolerance ..",
						content: "in the face of dualities such as happiness and distress, or cold and warmth to become free from anxieties regarding gain and loss",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/gita-119.jpg',
							w: 600,
							h: 403,
						
						}

					},
					
					{
					
						heading: "You have the right to work, but..",
						content: "never to the fruit of work. You should never engage in action for the sake of reward.",
						muted: 'Krishna',
						image: {
						
						
							src: 'static/images/maxresdefault.jpg',
							w: 1028,
							h: 874,
						
						},

					},
					
					
					{
					
						heading: "Do your Dharma and leave..",
						content: "the results to Krishna. Unwise are constantly anxious about the results of what they do.",
						muted: 'Krishna',
						image: {
						
							src: 'static/images/Krishna Childhhod.jpg',
							w: 490,
							h: 390,
						
						},

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
				
				EventBus.$emit("add-to-gallary", item.image);
				
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
			
				var that = this;
				
				this.getImageColor(this.firstSlideContent.image).then(function(c){
				
					that.showSlider= true;
				
					setTimeout(function(){
					
						that.createSlider();	

						that.applyColor(1,c);
					
					}, 1)						
				
				});
				
			},
			
			
			
			createSlider(){
				
				var that = this,
				$navArrows = $( '#nav-arrows' );
				
				this.slitslider = $( '#slider' ).slitslider( {
					onBeforeChange : function( slide, pos ) { 
					
						
					},
					
					onAfterChange: function(slide, pos){
						
						var $nav = that.getNav();

						$nav.removeClass( 'nav-dot-current' );
						$nav.eq( pos ).addClass( 'nav-dot-current' );
							
						//that.applySlideColor(pos);	
					
					},
					
				});
						
												
				// add navigation events
				$navArrows.children( ':last' ).on( 'click', function() {

					that.slitslider.next();
					
					return false;
					
			
				});
				
				$navArrows.children( ':first' ).on( 'click', function() {
								
					that.slitslider.previous();
					return false;

				});
				
			
			
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
			
			
			getImage(pos){
			
				return $(".img-"+(pos));
			
			},
			
			applyColor(pos, color){
			
				var img = this.getImage(pos);
			
				img.parents(".sl-slide-inner:first").css({
									
					background: color,
													
				});
						
			},
			
			applySlideColor(pos){
				
				var img = this.getImage(pos),
					that = this;
				
				img.one("load", function(){
				
					that.getImageColor(img[0]).then(function(color){
					
						that.applyColor(pos, color);
						
						EventBus.$emit("close-mic-popup");
						
						that.slitslider.jump(pos);
											
						
					});				
			
				});
			
			
			},

			
			getImageColor(img){
			
				return new Promise(function(resolve, reject){
				
					RGBaster.colors(img, 
						{
							success: function(payload) {				
							
								resolve(payload.dominant);
											
							}
						});
							
				});
							
			},
			
			addNewSlide(obj){
				
				var that = this;
				
				this.slideIndex++;

				var items = $('<div class="sl-slide"  data-orientation="'+ (that.slideIndex%2==0? "horizontal": "vertical") +'" data-slice1-rotation="'+that.getRandomInteger()+'" data-slice2-rotation="'+that.getRandomInteger()+'" data-slice1-scale="'+that.getRandomInteger(2)+'" data-slice2-scale="'+that.getRandomInteger(2)+'" ><div class="sl-slide-inner"><div class="deco"><div class="circle"><img class="img-'+that.slideIndex+' content-image br" src="'+obj.image.src+'"  /></div></div><h2>'+obj.heading+'</h2><blockquote><p>'+obj.content+'</p><cite>'+obj.muted+'</cite></blockquote></div></div>');
				
				this.slitslider.add(items);
							
				this.applySlideColor(this.slideIndex);
					
	
			},	
			
			pushNewSlide(){
					
				var obj = this.getNewSlideContent();
									
				this.addNewSlide(obj);
			
			},
			
			initGallary(){
			
				alert("d");
			
			},
			
		
		},
		
		
	}
	
	export default slider;

</script>