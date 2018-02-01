<template>
	
	<div>
	
	<div class="speak-button">
		<img :id="elementId" :class="{glow: glow}" @click="clicked()" src="static/images/speak.png" />
	</div>
		
		
		

<button id="btn">Open PhotoSwipe</button>

<!-- Root element of PhotoSwipe. Must have class pswp. -->
<div class="pswp" tabindex="-1" role="dialog" aria-hidden="true">

    <!-- Background of PhotoSwipe. 
         It's a separate element, as animating opacity is faster than rgba(). -->
    <div class="pswp__bg"></div>

    <!-- Slides wrapper with overflow:hidden. -->
    <div class="pswp__scroll-wrap">

        <!-- Container that holds slides. PhotoSwipe keeps only 3 slides in DOM to save memory. -->
        <div class="pswp__container">
            <!-- don't modify these 3 pswp__item elements, data is added later on -->
            <div class="pswp__item"></div>
            <div class="pswp__item"></div>
            <div class="pswp__item"></div>
        </div>

        <!-- Default (PhotoSwipeUI_Default) interface on top of sliding area. Can be changed. -->
        <div class="pswp__ui pswp__ui--hidden">

            <div class="pswp__top-bar">

                <!--  Controls are self-explanatory. Order can be changed. -->

                <div class="pswp__counter"></div>

                <button class="pswp__button pswp__button--close" title="Close (Esc)"></button>

                <button class="pswp__button pswp__button--share" title="Share"></button>

                <button class="pswp__button pswp__button--fs" title="Toggle fullscreen"></button>

                <button class="pswp__button pswp__button--zoom" title="Zoom in/out"></button>

                <!-- Preloader demo https://codepen.io/dimsemenov/pen/yyBWoR -->
                <!-- element will get class pswp__preloader--active when preloader is running -->
                <div class="pswp__preloader">
                    <div class="pswp__preloader__icn">
                      <div class="pswp__preloader__cut">
                        <div class="pswp__preloader__donut"></div>
                      </div>
                    </div>
                </div>
            </div>

            <div class="pswp__share-modal pswp__share-modal--hidden pswp__single-tap">
                <div class="pswp__share-tooltip"></div> 
            </div>

            <button class="pswp__button pswp__button--arrow--left" title="Previous (arrow left)">
            </button>

            <button class="pswp__button pswp__button--arrow--right" title="Next (arrow right)">
            </button>

            <div class="pswp__caption">
                <div class="pswp__caption__center"></div>
            </div>

          </div>

        </div>

</div>


		
		
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
			
			
			
			
			
			
			
			
			
			
			var openPhotoSwipe = function() {
    var pswpElement = document.querySelectorAll('.pswp')[0];

    // build items array
    var items = [
        {
            src: 'https://farm2.staticflickr.com/1043/5186867718_06b2e9e551_b.jpg',
            w: 964,
            h: 1024
        },
        {
            src: 'https://farm7.staticflickr.com/6175/6176698785_7dee72237e_b.jpg',
            w: 1024,
            h: 683
        }
    ];
    
    // define options (if needed)
    var options = {
             // history & focus options are disabled on CodePen        
        history: false,
        focus: false,

        showAnimationDuration: 0,
        hideAnimationDuration: 0
        
    };
    
    var gallery = new PhotoSwipe( pswpElement, PhotoSwipeUI_Default, items, options);
    gallery.init();
};

openPhotoSwipe();

document.getElementById('btn').onclick = openPhotoSwipe;
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
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