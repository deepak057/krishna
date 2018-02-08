<template>

	<div>
		<img @click="showInfoPopup" src="static/images/info.png" class="info-icon" title="Help, about, more info etc"/>
		
		
		<bootstrap-modal centered  role="dialog" class="info-popup-custom" ref="infoModal" :need-header="true" :need-footer="false">
			<div slot="title">
				
				Info: Krishna, the Supreme 
				
			</div>
			<div slot="body">
					
					<div class="container">
						<div class="row">
							<div >
								<div class="col-lg-3 col-md-3 col-sm-3 col-xs-3 bhoechie-tab-menu">
								  <div class="list-group">
									<a href="#" class="list-group-item active text-center">
									  <h4 class="glyphicon glyphicon-info-sign"></h4><br/>About
									</a>
									<a href="#" class="list-group-item text-center">
									  <h4 class="glyphicon glyphicon-question-sign"></h4><br/>Help
									</a>
									<a href="#" class="list-group-item text-center">
									  <h4 class="glyphicon glyphicon-earphone"></h4><br/>Contact
									</a>
									
								  </div>
								</div>
								<div class="col-lg-9 col-md-9 col-sm-9 col-xs-9 bhoechie-tab">
									<!-- flight section -->
									<div class="bhoechie-tab-content active">
										
										
										

										  <!-- Introduction Row -->
										  <h1 class="my-4">About Us
											<small>It's Nice to Meet You!</small>
										  </h1>
										  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sint, explicabo dolores ipsam aliquam inventore corrupti eveniet quisquam quod totam laudantium repudiandae obcaecati ea consectetur debitis velit facere nisi expedita vel?</p>

										  <!-- Team Members Row -->
										  <div class="row">
											<div class="col-lg-12">
											  <h2 class="my-4">Our Team</h2>
											</div>
											<div class="col-lg-4 col-sm-6 text-center mb-4">
											  <img class="rounded-circle img-fluid d-block mx-auto" src="http://placehold.it/200x200" alt="">
											  <h3>John Smith
												<small>Job Title</small>
											  </h3>
											  <p>What does this team member to? Keep it short! This is also a great spot for social links!</p>
											</div>
											<div class="col-lg-4 col-sm-6 text-center mb-4">
											  <img class="rounded-circle img-fluid d-block mx-auto" src="http://placehold.it/200x200" alt="">
											  <h3>John Smith
												<small>Job Title</small>
											  </h3>
											  <p>What does this team member to? Keep it short! This is also a great spot for social links!</p>
											</div>
											<div class="col-lg-4 col-sm-6 text-center mb-4">
											  <img class="rounded-circle img-fluid d-block mx-auto" src="http://placehold.it/200x200" alt="">
											  <h3>John Smith
												<small>Job Title</small>
											  </h3>
											  <p>What does this team member to? Keep it short! This is also a great spot for social links!</p>
											</div>
											<div class="col-lg-4 col-sm-6 text-center mb-4">
											  <img class="rounded-circle img-fluid d-block mx-auto" src="http://placehold.it/200x200" alt="">
											  <h3>John Smith
												<small>Job Title</small>
											  </h3>
											  <p>What does this team member to? Keep it short! This is also a great spot for social links!</p>
											</div>
											<div class="col-lg-4 col-sm-6 text-center mb-4">
											  <img class="rounded-circle img-fluid d-block mx-auto" src="http://placehold.it/200x200" alt="">
											  <h3>John Smith
												<small>Job Title</small>
											  </h3>
											  <p>What does this team member to? Keep it short! This is also a great spot for social links!</p>
											</div>
											<div class="col-lg-4 col-sm-6 text-center mb-4">
											  <img class="rounded-circle img-fluid d-block mx-auto" src="http://placehold.it/200x200" alt="">
											  <h3>John Smith
												<small>Job Title</small>
											  </h3>
											  <p>What does this team member to? Keep it short! This is also a great spot for social links!</p>
											</div>
										  </div>

    
										
										
										
									</div>
									<!-- train section -->
									<div class="bhoechie-tab-content">
										<center>
										  <h1 class="glyphicon glyphicon-road" style="font-size:12em;color:#55518a"></h1>
										  <h2 style="margin-top: 0;color:#55518a">Cooming Soon</h2>
										  <h3 style="margin-top: 0;color:#55518a">Train Reservation</h3>
										</center>
									</div>
						
									<!-- hotel search -->
									<div class="bhoechie-tab-content">
										<center>
										  <h1 class="glyphicon glyphicon-home" style="font-size:12em;color:#55518a"></h1>
										  <h2 style="margin-top: 0;color:#55518a">Cooming Soon</h2>
										  <h3 style="margin-top: 0;color:#55518a">Hotel Directory</h3>
										</center>
									</div>
									<div class="bhoechie-tab-content">
										<center>
										  <h1 class="glyphicon glyphicon-cutlery" style="font-size:12em;color:#55518a"></h1>
										  <h2 style="margin-top: 0;color:#55518a">Cooming Soon</h2>
										  <h3 style="margin-top: 0;color:#55518a">Restaurant Diirectory</h3>
										</center>
									</div>
									<div class="bhoechie-tab-content">
										<center>
										  <h1 class="glyphicon glyphicon-credit-card" style="font-size:12em;color:#55518a"></h1>
										  <h2 style="margin-top: 0;color:#55518a">Cooming Soon</h2>
										  <h3 style="margin-top: 0;color:#55518a">Credit Card</h3>
										</center>
									</div>
								</div>
							</div>
					  </div>
					
									
				</div>
			</div>
		</bootstrap-modal> 
	
	
	</div>
	
</template>

<script>

	export default {
	
		components: {
		
			'bootstrap-modal': require('vue2-bootstrap-modal')
		
		},
	
	
		name: 'info',
		
		mounted(){
		
			$("div.bhoechie-tab-menu>div.list-group>a").click(function(e) {
				e.preventDefault();
				$(this).siblings('a.active').removeClass("active");
				$(this).addClass("active");
				var index = $(this).index();
				$("div.bhoechie-tab>div.bhoechie-tab-content").removeClass("active");
				$("div.bhoechie-tab>div.bhoechie-tab-content").eq(index).addClass("active");
			});
		
		},
		
		methods: {
		
			showInfoPopup(){
			
				this.$refs.infoModal.open();

			
			},
		
		}
		
	
	}

</script>

