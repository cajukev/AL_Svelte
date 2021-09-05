<script context="module">
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ page, fetch, session, context }) {
		const path = page.path;

		return {
			props: {
				path
			}
		};
	}
</script>

<script>
	import Header from '../components/header.svelte';
	import Footer from '../components/footer.svelte';
	import PageTransition from '../components/utils/PageTransition.svelte';
	import { beforeUpdate, onMount } from 'svelte';
	import { lang } from '../stores.js';
	import { page } from '../stores.js';
	export let path;
	onMount(() => {
		console.log('layout')
	})
	beforeUpdate(() => {
		if (path.length >= 2 && path.slice(-2) == 'en') {
			lang.set('en');
			if (path.slice(1, -3) == 'galerie') {
				page.set('galerie');
			} else {
				page.set('');
			}
		} else {
			lang.set('fr');
			if (path.length >= 2) {
				if (path.slice(-7) == 'galerie') {
					page.set('galerie');
				} else {
					page.set('');
				}
			} else {
				page.set('');
			}
		}
		console.log($page);
	});
</script>

<div>
	<div class="background" />
	<Header />
	<PageTransition refresh={path}>
		<slot />
	</PageTransition>
	<Footer />
	<div class="filter" />
</div>


<style lang="scss">
	:global(*) {
		box-sizing: border-box;
	}
	:global(html) {
		background-color: #252527;
		max-width: 100%;
		min-height: 100%;
		position: relative;
	}
	:global(body) {
		margin: 0px;
		padding: 0px;
	}
	:global(html::after) {
		content: '';
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		box-shadow: inset 0px 0px calc(max(50px, 3rem)) rgba(255, 255, 255, 0.25);
		pointer-events: none;
	}
	:global(p),
	:global(a),
	:global(label),
	:global(input),
	:global(textarea),
	:global(button) {
		/* https://www.sitepoint.com/eight-definitive-font-stacks-2/?_ga=2.261681806.221548906.1620436002-626617126.1619641332 */
		font-family: Geneva, 'Helvetica Neue', Helvetica, Arial, sans-serif;
		margin: 0px;
		font-weight: 300;
		color: white;
		font-size: 1rem;
	}
	:global(p) {
		line-height: 140%;
		text-shadow: 0 0.15rem 0.15rem #060606;
	}
	:global(h1),
	:global(h2) {
		/* https://www.sitepoint.com/eight-definitive-font-stacks/?_ga=2.255914888.221548906.1620436002-626617126.1619641332 */
		font-family: Constantia, 'Lucida Bright', Lucidabright, 'Lucida Serif', Lucida, 'DejaVu Serif',
			'Bitstream Vera Serif', 'Liberation Serif', Georgia, serif;
		font-weight: 400;
		margin: 0px;
		color: white;
		@media (max-width: 1024px) {
			text-align: center;
		}
	}
	:global(h1){
		text-shadow: 0.5rem 0.5rem 0.15rem #060606;
	}
	:global(h2){
		text-shadow: 0.25rem 0.25rem 0.075rem #060606;
	}
	:global(a) {
		text-decoration: underline;
		text-decoration-color: white;
	}
	/*  FONT SIZING QUERIES  */
	@media (max-width: 420px) {
		:global(html) {
			font-size: 1rem;
		}
		:global(h1) {
			font-size: 1.5rem;
		}
		:global(h2) {
			font-size: 1.25rem;
		}
	}
	@media (min-width: 421px) {
		:global(html) {
			font-size: calc(1rem + 0.3vw);
		}
		:global(h1) {
			font-size: calc(2.1rem + 0.3vw);
		}
		:global(h2) {
			font-size: calc(1.8rem + 0.3vw);
		}
	}
	@media (min-width: 1921px) {
		:global(html) {
			font-size: calc(1rem + 0.6vw);
		}
		:global(h1) {
			font-size: calc(2.1rem + 0.6vw);
		}
		:global(h2) {
			font-size: calc(1.8rem + 0.6vw);
		}
	}
	/*  LAYOUT QUERIES  */

	@media (max-width: 600px) {
		:global(.contained) {
			padding: 0px 0.75rem;
		}
	}
	@media (min-width: 601px) and (max-width: 1024px) {
		:global(body) {
			
		}
		:global(.contained) {
			padding: 0px calc(1rem + 5vw);
			width: 100%;
		}
	}
	@media (min-width: 1025px) {
		:global(.l_contained) {
			margin-left: 6rem;
		}
		:global(.header::after) {
			content: '';
			position: fixed;
			top: 0;
			left: 0;
			z-index: -1;
			width: 2rem;
			height: 100%;
			background-color: #343434;
		}
	}
</style>
