<template>

	<div>
	
		<info></info>
		<chant_button></chant_button>		
			
	
	</div>

</template>

<script>

	import { ChantButton } from '../../chant_button/components';
	import { Info } from '../../info/components';


	export default {
	
		components: {
		
			"chant_button": ChantButton,
			Info,

		
		},
	
		name: 'navigation',
		
	
	}

</script>