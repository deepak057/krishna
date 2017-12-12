<template>
  <div id="app">
	
	
        <dashboard></dashboard>
		
	
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
  }
}
</script>

<style>

</style>
