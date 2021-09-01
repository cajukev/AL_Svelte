<script>
	import Header from '../components/header.svelte';
</script>

<div class="container">
	<Header />
	<p class='contained l_contained'>761 Boulevard Saint Jean Baptiste, Mercier, Quebec</p>
</div>

<style lang="scss">
	@media (max-width: 1024px) {
		.container {
			background-color: #343434;
			width: 100%;
			margin-top: 3rem;
			padding-bottom: 3rem;
		}
	}
	@media (min-width: 1025px) {
		.container {
			background-color: #343434;
			width: 100%;
      margin-top: 3rem;
			padding-bottom: 3rem;
		}
	}
</style>
