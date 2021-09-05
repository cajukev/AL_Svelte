<script>
	import { album } from '/static/contenu.js';
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';
	let nbcategories = album.categories.length;
	let close;
	export let currentcategory = 0;
	export let currentpicture = 0;
	export let visible;

	onMount(() => {
		console.log(album.categories);
	});

	$: console.log(`${currentcategory},${currentpicture}`);
	$: if (close) close.focus();
</script>

{#if visible == true}
	<div class="container" in:fly={{ y: 500, duration: 750 }} out:fly={{ y: 500, duration: 400 }}>
		<div class="bg" on:click={() => (visible = false)} />
		<div class="grid">
			<div
				class="close"
				tabindex="0"
				role="button"
				bind:this={close}
				on:click={() => (visible = false)}
				on:keypress={(e) => {
					if (e.charCode === 13) visible = false;
				}}
			>
				<p>Retour vue grille</p>
				<svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path
						d="M0 0V10.6667H10.6667V0H0ZM8 8H2.66667V2.66667H8V8ZM0 13.3333V24H10.6667V13.3333H0ZM8 21.3333H2.66667V16H8V21.3333ZM13.3333 0V10.6667H24V0H13.3333ZM21.3333 8H16V2.66667H21.3333V8ZM13.3333 13.3333V24H24V13.3333H13.3333ZM21.3333 21.3333H16V16H21.3333V21.3333Z"
						fill="white"
					/>
				</svg>
			</div>
			<div class="photo">
				<picture>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-400.webp, op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-800.webp 2x"
						media="(max-width:400px)"
						type="image/webp"
						num
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-400.jpg, op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-800.webp 2x"
						media="(max-width:400px)"
						type="image/jpeg"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-600.webp, op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1200.webp 2x"
						media="(max-width:600px)"
						type="image/webp"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-600.jpg, op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1200.webp 2x"
						media="(max-width:600px)"
						type="image/jpeg"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1200.webp, op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1600.webp 2x"
						media="(max-width:1024px)"
						type="image/webp"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1200.jpg, op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1600.webp 2x"
						media="(max-width:1024px)"
						type="image/jpeg"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-800.webp "
						media="(max-width:1280)"
						type="image/webp"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-800.jpg "
						media="(max-width:1280px)"
						type="image/jpeg"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1200.webp "
						media="(max-width:1920px)"
						type="image/webp"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1200.jpg "
						media="(max-width:1920px)"
						type="image/jpeg"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1600.webp "
						type="image/webp"
					/>
					<source
						srcset="op{album.categories[currentcategory - 1].photos[currentpicture - 1]
							.id}-1600.jpg "
						type="image/jpeg"
					/>
					<img
						src="op{album.categories[currentcategory - 1].photos[currentpicture - 1].id}-400.jpg"
						alt="hi:)"
					/>
				</picture>
			</div>
			<div class="prev">
				<div
					tabindex="0"
					role="button"
					class="navphoto {currentpicture == 1 ? 'disabled' : ''}"
					on:click={() => (currentpicture -= 1)}
					on:keypress={(e) => {
						if (e.charCode === 13) currentpicture = currentpicture - 1;
					}}
				>
					<svg viewBox="0 0 23 41" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path
							d="M21 41L23 38.8519L3.53901 20.4533L23 2.05467L21 0L0 19.7995V21.0137L21 41Z"
							fill="white"
						/>
					</svg>
					<p>Photo</p>
				</div>
				<div
					tabindex="0"
					role="button"
					class="navcategorie {currentcategory == 1 ? 'disabled' : ''}"
					on:click={() => {currentcategory -= 1;currentpicture=1}}
					on:keypress={(e) => {
						if (e.charCode === 13) {currentcategory -= 1;currentpicture=1}
					}}
				>
					<svg viewBox="0 0 23 41" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path
							d="M21 41L23 38.8519L3.53901 20.4533L23 2.05467L21 0L0 19.7995V21.0137L21 41Z"
							fill="white"
						/>
					</svg>
					<p>Catégorie</p>
				</div>
			</div>
			<div class="next">
				<div
					tabindex="0"
					role="button"
					class="navphoto {currentpicture == album.categories[currentcategory - 1].photos.length
						? 'disabled'
						: ''}"
					on:click={() => (currentpicture += 1)}
					on:keypress={(e) => {
						if (e.charCode === 13) currentpicture += 1;
					}}
				>
					<p>Photo</p>
					<svg viewBox="0 0 23 41" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path
							d="M2 41L0 38.8519L19.461 20.4533L0 2.05467L2 0L23 19.7995V21.0137L2 41Z"
							fill="white"
						/>
					</svg>
				</div>
				<div
					tabindex="0"
					role="button"
					class="navcategorie {currentcategory == album.categories.length ? 'disabled':''}"
					on:blur={close.focus()}
					on:click={() => {currentcategory += 1;currentpicture = 1}}
					on:keypress={(e) => {
						if (e.charCode === 13) {currentcategory += 1;currentpicture = 1;}
					}}
				>
					<p>Catégorie</p>
					<svg viewBox="0 0 23 41" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path
							d="M2 41L0 38.8519L19.461 20.4533L0 2.05467L2 0L23 19.7995V21.0137L2 41Z"
							fill="white"
						/>
					</svg>
				</div>
			</div>
			<div class="text">
				<p class="categorie">{album.categories[currentcategory - 1].nom}</p>
				<p class="photonom">
					<b>{album.categories[currentcategory - 1].photos[currentpicture - 1].nom}</b>
				</p>
				<p class="photodesc">
					{album.categories[currentcategory - 1].photos[currentpicture - 1].desc}
				</p>
			</div>
		</div>
	</div>
{/if}

<style lang="scss">
	.container {
		position: fixed;
		top: 0;
		left: 0;
		height: 100vh;
		overflow-y: scroll;
		width: 100%;
		background: #000000b2;
		backdrop-filter: blur(0.35rem);
		color: #fff;
		z-index: 2;
		&::-webkit-scrollbar {
			display: none;
		}
		-ms-overflow-style: none;
		scrollbar-width: none;
		& .bg {
			position: absolute;
			top: 0;
			width: 100%;
			height: 100%;
			z-index: -1;
		}
		& .grid {
			display: grid;
			pointer-events: none;
			& .close {
				display: flex;
				flex-direction: row;
				align-items: center;
				justify-content: center;
				text-decoration: underline;
				cursor: pointer;
				pointer-events: all;
				& svg {
					height: 1.5rem;
					margin-left: 1rem;
				}
			}
			& .prev,
			.next {
				display: flex;
				flex-direction: column;
				& .navphoto,
				.navcategorie {
					pointer-events: all;
					display: flex;
					flex-direction: row;
					padding: 1rem 0rem;
					cursor: pointer;
					&.disabled {
						opacity: 0.5;
					}
				}
				& svg {
					height: 1.5rem;
				}
			}
			.prev {
				& .navphoto > p,
				.navcategorie > p {
					margin-left: 1rem;
				}
			}
			.next {
				& .navphoto > p,
				.navcategorie > p {
					margin-right: 1rem;
				}
				& > .navphoto,
				> .navcategorie {
					justify-content: flex-end;
				}
			}
			& .photo {
				align-self: center;
				justify-self: center;
				pointer-events: all;

				& img {
					width: 100%;
				}
			}
			& .text {
				& p {
					pointer-events: all;
					&.categorie {
						font-size: 1.2rem;
						font-style: italic;
						width: fit-content;
					}
					&.photonom {
						font-size: 1.2rem;
						width: fit-content;
					}
				}
			}
		}
	}
	@media (max-width: 1024px) {
		.grid {
			display: grid;
			grid-template-columns: repeat(2, 50%);
			& .close {
				grid-area: 1 / 1 / span 1 / span 2;
				margin-top: 2rem;
			}
			& .prev {
				grid-area: 3 / 1 / span 1 / span 1;
				margin-left: calc(1rem + 5vw);
				margin-top: 1rem;
				@media (max-width: 600px) {
					margin-left: 0.75rem;
				}
			}
			& .next {
				grid-area: 3 / 2 / span 1 / span 1;
				margin-right: calc(1rem + 5vw);
				margin-top: 1rem;
				@media (max-width: 600px) {
					margin-right: 0.75rem;
				}
			}
			& .photo {
				grid-area: 2 / 1 / span 1 / span 2;
				width: 100%;
				margin-top: 2rem;
			}
			& .text {
				grid-area: 4 / 1 / span 1 / span 2;
				margin: 2rem calc(1rem + 5vw) 0 calc(1rem + 5vw);
				margin-top: 2rem;
				margin-bottom: 2rem;
				@media (max-width: 600px) {
					margin: 2rem 0.75rem 0 0.75rem;
				}
				& p {
					&.categorie {
					}
					&.photonom {
						margin-top: 1rem;
					}
					&.photodesc {
						margin-top: 1rem;
					}
				}
			}
		}
	}
	@media (min-width: 1025px) {
		.grid {
			display: grid;
			grid-template-columns: repeat(3, auto);
			grid-template-rows: repeat(3, auto);
			& .close {
				grid-area: 1 / span 3 /1 / span 1;
				margin-top: 2rem;
			}
			& .prev {
				grid-column: 1 / span 1;
				grid-row: 2 / span 1;
				align-self: center;
				margin: auto;
			}
			& .photo {
				grid-column: 2 / span 1;
				grid-row: 2 / span 1;
				max-width: 60vw;
				border: 0.2rem solid white;
				margin-top: 2rem;
				& picture {
					height: 100%;
					& img {
						display: block;
					}
				}
			}
			& .next {
				grid-column: 3 / span 1;
				grid-row: 2 / span 1;
				align-self: center;
				justify-self: end;
				margin: auto;
			}
			& .text {
				grid-column: 2 / span 1;
				grid-row: 3 / span 1;
				max-width: 60vw;
				align-self: start;
				justify-self: center;
				width: 100%;
				display: grid;
				grid-template-columns: 20% 80%;
				align-content: start;
				margin-top: 2rem;
				margin-bottom: 2rem;
				& p {
					font-size: 1rem;
					&.categorie {
						grid-area: 1 / 1 / span 1 / span 1;
						width: 8rem;
					}
					&.photonom {
						grid-area: 1 / 2 / span 1 / span 1;
						margin-bottom: 1rem;
						
					}
					&.photodesc {
						grid-area: 2 / 2 / span 1 / span 1;
						
					}
				}
			}
		}
	}
</style>
