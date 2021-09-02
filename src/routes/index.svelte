<script>
	import Hero from '../components/hero/hero.svelte';
	import Thumbnails from '../components/hero/thumbnails.svelte';
	import Form from '../components/form.svelte';
	import { onMount } from 'svelte';
	import { navigated } from '../stores';
	let btf_container;
	function scrollEvent() {
		console.log('scroll');
		btf_container.style.opacity = 1;
		btf_container.style.transform = 'none';
	}
	onMount(() => {
		if (window.scrollY != 0 || $navigated) scrollEvent();
	});
</script>

<svelte:window on:scroll|once={scrollEvent} />

<div class="atf_container">
	<h1 class="contained">Vos armoires sur mesure depuis 1979</h1>

	<div id="hero_component">
		<Hero />
	</div>
	<div class="thumbnails contained" id="thumbnails1">
		<Thumbnails />
	</div>
	<p class="contained">
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Consectetur sed tortor enim cras
		viverra egestas. Est elementum sed pellentesque orci risus.
		<br /><br />
		suspendisse nibh diam laoreet sed nisl in sit. Bibendum integer ultricies vestibulum tristique urna
		amet. Amet non et ipsum accumsan, ac ultrices. Neque urna lorem nulla sagittis blandit.
	</p>
</div>
<div />
<div  class="galerie_lien contained">
	<a href="/galerie">Visiter la galerie de photos</a>
	<svg viewBox="0 0 33 34" fill="none" xmlns="http://www.w3.org/2000/svg">
		<path
			d="M29.3333 3.77778V30.2222H3.66667V3.77778H29.3333ZM29.3333 0H3.66667C1.65 0 0 1.7 0 3.77778V30.2222C0 32.3 1.65 34 3.66667 34H29.3333C31.35 34 33 32.3 33 30.2222V3.77778C33 1.7 31.35 0 29.3333 0ZM20.4233 16.7356L14.9233 24.0456L11 19.1533L5.5 26.4444H27.5L20.4233 16.7356Z"
			fill="white"
		/>
	</svg>
</div>
<div bind:this={btf_container} class="btf_container contained l_contained">
	<picture>
		<source srcset="op1-400.webp, op1-800.webp 2x" media="(max-width:500px)" type="image/webp" />
		<source srcset="op1-400.jpg, op1-800.webp 2x" media="(max-width:500px)" type="image/jpeg" />
		<source srcset="op1-600.webp, op1-1200.webp 2x" media="(max-width:768px)" type="image/webp" />
		<source srcset="op1-600.jpg, op1-1200.webp 2x" media="(max-width:768px)" type="image/jpeg" />
		<source srcset="op1-800.webp " media="(max-width:1280)" type="image/webp" />
		<source srcset="op1-800.jpg " media="(max-width:1280px)" type="image/jpeg" />
		<source srcset="op1-1200.webp " media="(max-width:1920px)" type="image/webp" />
		<source srcset="op1-1200.jpg " media="(max-width:1920px)" type="image/jpeg" />
		<source srcset="op1-1600.webp " type="image/webp" />
		<source srcset="op1-1600.jpg " type="image/jpeg" />
		<img src="op1-400.jpg" alt="hi:)" />
	</picture>
	<h2>Discutions de votre future cuisine!</h2>
	<div class="form_container">
		<Form class="form"/>
	</div>
</div>

<style lang="scss">

	@media (max-width: 1024px) {
		.atf_container {
			& h1,
			#hero_component,
			p {
				margin-top: 2rem;
			}
		}
		.btf_container {
			margin-top: 2rem;
			& img {
				display: none;
			}
			& h2{
				text-align: initial;
			}
		}
	}
	@media (min-width: 1025px) {
		.atf_container {
			display: grid;
			grid-template-columns: 40% 60%;
			margin-top: 3rem;
			margin-left: 6rem;
			margin-right: 3rem;
			filter: drop-shadow(0px 0.25rem 0.5rem rgba(0, 0, 0, 0.75));
			h1 {
				margin-right: 2rem;
				margin-bottom: 2rem;
				@media (max-width: 1220px) {
					grid-area: 1 / 1 / span 1 / span 2;
				}
			}
			p {
				margin-right: 2rem;
				margin-bottom: 2rem;
			}
			& p {
				@media (max-width: 1499px) {
					grid-area: 2 / 1 / span 2 / span 1;
					align-self: center;
					margin-bottom: 0;
					line-height: calc(125% + 0.5vw);
				}
			}
			& #hero_component {
				grid-area: 1 / 2 / span 3 / span 1;

				@media (max-width: 1499px) {
					grid-area: 1 / 2 / span 2 / span 1;
					align-self: end;
				}
				@media (min-width: 1500px) {
					align-self: center;
				}
				@media (max-width: 1220px) {
					grid-area: 2 / 2 / span 1 / span 2;
				}
			}
		}
		.btf_container {
			margin-top: 2rem;
			display: grid;
			grid-template-columns: 60% 40%;
			opacity: 0.25;
			transform: translateY(1rem);
			transition: transform 2s ease, opacity 1s ease;
			& picture {
				margin-right: 2rem;
				align-self: flex-start;
				grid-area: 1 / 1 / span 3 / span 1;
				filter: drop-shadow(0px 1rem 2rem rgba(0, 0, 0, 0.75));	
				@media (max-width: 1449px) {
					grid-area: 2 / 1 / span 1 / span 1;
					margin-top: 1rem;
				}
				& img {
					width: 100%;
				}
			}
			& h2 {
				margin-right: 3rem;
				@media (max-width: 1449px) {
					grid-area: 1 / 1 / span 1 / span 2;
					justify-self: start;
				}
			}
		}
	}
	.galerie_lien {
		display: flex;
		margin-top: 2rem;
		align-items: center;
		justify-content: center;
		filter: drop-shadow(0.25rem 0.25rem 0.125rem rgba(0,0,0,0.75));
		& a{
			font-size: 1.2rem;
		}
		& svg {
			height: 1.5rem;
			margin-left: 1rem;
		}
	}
	.thumbnails {
		width: 100%;
		display: grid;

		@media (min-width: 1500px) {
			grid-area: 3 / 1 / span 1 / span 1;
			align-self: end;
		}
		@media (max-width: 1499px) {
			grid-area: 3 / 2 / span 1 / span 1;
			margin-top: 1rem;
		}
		@media (max-width: 1499px) {
			align-self: start;
			margin-top: 1rem;
		}
	}
</style>
