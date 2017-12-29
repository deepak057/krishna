<template>
  <div id="app">
			
		<dashboard></dashboard>
		
  </div>
</template>

<script>

import { Dashboard } from './dashboard/components';

export default {
  name: 'app',
  components: {
	Dashboard,
  },
  
}
</script>

<style>

</style>
