<template>

	<div>
		<img @click="showInfoPopup" src="static/images/info.png" class="info-icon" title="Help, about, more info etc"/>
		
		
		<bootstrap-modal centered  role="dialog" class="info-popup-custom" ref="infoModal" :need-header="false" :need-footer="false">
			<div slot="title">
				
				About
				
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
									<!--<a href="#" class="list-group-item text-center">
									  <h4 class="glyphicon glyphicon-question-sign"></h4><br/>Help
									</a>-->
									<a href="#" class="list-group-item text-center">
									  <h4 class="glyphicon glyphicon-earphone"></h4><br/>Contact
									</a>
									
								  </div>
								</div>
								<div class="col-lg-9 col-md-9 col-sm-9 col-xs-9 bhoechie-tab">
									<!-- flight section -->
									<div class="bhoechie-tab-content active">
											

										  <!-- Introduction Row -->
										  <h1 class="my-4">About The Site
										
										  </h1>
										  
										  
										  <div>
										  
											 <p> 
												In today's world, people don't have time for nor interest in spiritual realization. Though I believe most will admit that spiritual engagement can make our lives better but to an intellectual and modern mind of this age, the ways religions require us to worship different kind of lords in different ways, does not make sense and so we never indulge in or want to explore real spiritualism that Geeta wanted mankind to do.
												
											</p>	
											
											<p>
											
												The quickest way to achieve spiritual realization ( or in simple words to be perfect in art of living life) is to only chant this simple mahamantra-

											</p>
											
											
											<div class="info-chant-highlight text-center text-danger">
												Hare Krishna Hare Krishna, Krishna Krishna Hare Hare<br/>
												Hare Rama Hare Rama, Rama Rama Hare Hare
											
											</div>
											
											<p>
												This little site aims to get you to chant MahaMantra. You simply have to click the Mic button on top-right corner of the page to turn on your mic and then start chanting this mahamantra. When you chant correctly, an inspiring quote from Geeta unlocks along with a beautiful picture of Krishna. 
												
											</p>	

											<p>
												The quotes are succinct and still give you as much knowledge as entire chapter of Geeta. This knowledge revealed through quotes that you will unlock by chanting Mahamantra correctly will make you more spiritually aware and will lead you to have a better life. You will feel a new power and strength within you that will make the journey of live very easy and delightful. You will know exactly what you are, what you're supposed to do and how to do what. It will enlighten you.
											</p>	

											<p>
												Get used to chanting it and see the difference. You need to give only a few minutes of your time and unlock at least one quote everyday. No need to follow any religion, no need to watch the spiritual lecturers, no need to follow any Indian Guru, no need to worship, no need to follow any rituals. Just chant this Mahamantra a few times a day and you will advance on this path of spiritual realization and will achieve perfection in life.
											</p>	

											
											
										  
										</div>
										  
										  
										  

										  <!-- Team Members Row -->
										<!--  <div class="row">
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
										  </div> -->

    
										
										
										
									</div>
									<!-- train section -->
									<!--<div class="bhoechie-tab-content">
										
										
										<div class="container ">
										
										
											<h1 class="my-4">Help
												<small>It's Nice to Meet You!</small>
											</h1>
											<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sint, explicabo dolores ipsam aliquam inventore corrupti eveniet quisquam quod totam laudantium repudiandae obcaecati ea consectetur debitis velit facere nisi expedita vel?</p>

										
										
											<div class="panel-group" id="faqAccordion">
												<div class="panel panel-default ">
													<div class="panel-heading accordion-toggle question-toggle collapsed" data-toggle="collapse" data-parent="#faqAccordion" data-target="#question0">
														 <h4 class="panel-title">
															<a href="#" class="ing">Q: What is Lorem Ipsum?</a>
													  </h4>

													</div>
													<div id="question0" class="panel-collapse collapse" style="height: 0px;">
														<div class="panel-body">
															 <h5><span class="label label-primary">Answer</span></h5>

															<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five <a href="http://jquery2dotnet.com/" class="label label-success">http://jquery2dotnet.com/</a> centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
																</p>
														</div>
													</div>
												</div>
												<div class="panel panel-default ">
													<div class="panel-heading accordion-toggle collapsed question-toggle" data-toggle="collapse" data-parent="#faqAccordion" data-target="#question1">
														 <h4 class="panel-title">
															<a href="#" class="ing">Q: Why do we use it?</a>
													  </h4>

													</div>
													<div id="question1" class="panel-collapse collapse" style="height: 0px;">
														<div class="panel-body">
															 <h5><span class="label label-primary">Answer</span></h5>

															<p>It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal distribution of letters, as opposed to using 'Content here, content here', making it look like readable English. Many desktop publishing packages and web page editors now use Lorem Ipsum as their default model text, and a search for 'lorem ipsum' will uncover many web sites still in their infancy. Various versions have evolved over the years, sometimes by accident, sometimes on purpose (injected humour and the like).</p>
														</div>
													</div>
												</div>
												<div class="panel panel-default ">
													<div class="panel-heading accordion-toggle collapsed question-toggle" data-toggle="collapse" data-parent="#faqAccordion" data-target="#question2">
														 <h4 class="panel-title">
															<a href="#" class="ing">Q: Where does it come from?</a>
													  </h4>

													</div>
													<div id="question2" class="panel-collapse collapse" style="height: 0px;">
														<div class="panel-body">
															 <h5><span class="label label-primary">Answer</span></h5>

															<p>Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source. Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of "de Finibus Bonorum et Malorum" (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum, "Lorem ipsum dolor sit amet..", comes from a line in section 1.10.32.</p>
														</div>
													</div>
												</div>
												<div class="panel panel-default ">
													<div class="panel-heading accordion-toggle collapsed question-toggle" data-toggle="collapse" data-parent="#faqAccordion" data-target="#question3">
														 <h4 class="panel-title">
															<a href="#" class="ing">Q: Where can I get some?</a>
													  </h4>

													</div>
													<div id="question3" class="panel-collapse collapse" style="height: 0px;">
														<div class="panel-body">
															 <h5><span class="label label-primary">Answer</span></h5>

															<p>There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don't look even slightly believable. If you are going to use a passage of Lorem Ipsum, you need to be sure there isn't anything embarrassing hidden in the middle of text. </p>
														</div>
													</div>
												</div>
												
											</div>
											
										</div>
										
										
										
										
									</div>-->
						
									<!-- hotel search -->
									<div class="bhoechie-tab-content">
										  
										  <h2>What is on your mind?</h2>
										  
										  <p >Feel free to drop us an email at <a href="mailto: deakmisra@gmail.com"><b><u>deakmisra@gmail.com</u></b></a> and we will try to get back as soon as possible.</p>
										  
										
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
					
						
<div class="modal-footer">
        <button type="button" class="btn btn-default" @click="hideInfoPopup()" data-dismiss="modal">Close</button>
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
			
			hideInfoPopup(){
			
				this.$refs.infoModal.close();
			
			},
		
		}
		
	
	}

</script>

