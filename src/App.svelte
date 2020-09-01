<script lang="ts">
	import Home from './Home.svelte';
	import Cohorts from './Cohorts.svelte';
	import Router from 'svelte-spa-router';

	const routes = {
		'/cohorts2021': Cohorts,
		'*': Home,
	};


</script>

<Router routes={routes} />