<template>
  <div id="app">
	
		<navigation></navigation>
		
		<div  class="speak-button">
			<img @click="clicked()" src="static/images/speak.png" />
		</div>
        
		<dashboard></dashboard>
		
		<bootstrap-modal centered  class="custom-popup" role="dialog" ref="theModal" :need-header="true" :need-footer="false">
			<div slot="title">
			</div>
			<div slot="body">
				<div class="text-center">
					 <img src="static/images/mic.png" />
					<h1>Listening....</h1>
				</div>
			</div>
		</bootstrap-modal> 
	
  </div>
</template>

<script>

import { Navigation } from './navigation/components';
import { Sidebar } from './sidebar/components';
import { Dashboard } from './dashboard/components';

export default {
  name: 'app',
  components: {
	Navigation,
	Sidebar,
	Dashboard,
	'bootstrap-modal': require('vue2-bootstrap-modal')
  },
  data(){
  
	return {
	
		overlay: false,
	
	}
  
  },
  
  methods: {
	clicked(){
		
		  this.$refs.theModal.open()
		
	
	},
	
	
  },
  
  
}
</script>

<style>

</style>
