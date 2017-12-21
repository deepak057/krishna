<template>
  <div id="app">
	
		<navigation></navigation>
		
		<div v-show="!overlay" @click="clicked" class="speak-button">
			<img src="static/images/speak.png" />
		</div>
        <dashboard></dashboard>
		<div v-show="overlay" id="overlay"></div>
		
		<div v-show="overlay" class="overlay-content">
		
			<img class="pointer"  v-show="overlay" @click="overlay=!overlay" src="static/images/index.png" />
		
			<img src="static/images/mic.png" />
		
		</div>
		
	
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
  },
  data(){
  
	return {
	
		overlay: false,
	
	}
  
  },
  methods: {
	clicked(){
		
		
		this.overlay = true;
		
	
	},
  
  },
}
</script>

<style>

</style>
