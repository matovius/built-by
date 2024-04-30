<script lang="ts">
	import { onMount } from 'svelte';
	import { adjectives } from '$lib/adjectives';
	import AboutModal from '$lib/components/AboutModal.svelte';
	import Header from '$lib/components/Header.svelte';
	import { fly, scale } from 'svelte/transition';
	import { quadInOut, quintInOut } from 'svelte/easing';

	let showPage: boolean = false;

	let GeneratedWrapper: HTMLDivElement;
	let generatedText: string;
	
	let genTextOpacity: number = 1;
	let genTextRotation: string = '0deg';
	//let genTextTransitionDuration: number = 0;

	let isAboutModalOpen: boolean = false;

	function showGenerated() {
		setTimeout(() => {
			//genTextTransitionDuration = 250;
			genTextOpacity = 1;
			genTextRotation = '0deg';
		}, 500);
	}

	function toggleGenerated() {
		//genTextTransitionDuration = 0;
		genTextOpacity = 0;
		genTextRotation = '-90deg';

		setTimeout(() => {
			generatedText = getRandomAdjective();
			//genTextTransitionDuration = 250;
			genTextOpacity = 1;
			genTextRotation = '0deg';
		}, 500);
	}

	function getRandomAdjective(): string {
		let randomAdjective: string = adjectives[Math.floor(Math.random() * adjectives.length)];
		return randomAdjective;
	}

	onMount(() => {
		setTimeout(() => {
			generatedText = getRandomAdjective();
			showPage = true;
		}, 2000);
	});
</script>

<svelte:head>
	<title>Built By</title>
</svelte:head>

{#if showPage}
	<div class="about-container" transition:scale={{ delay: 500, duration: 500, easing: quintInOut, start: 0, opacity: 0 }}>
		<button
			class="button"
			on:click={() => {
				isAboutModalOpen = true;
			}}
		>
			<span>About</span>
		</button>
		<AboutModal bind:isOpen={isAboutModalOpen} />
	</div>
{/if}

<div class="container">
	<Header isPageLoaded={showPage} />


	{#if showPage}
		<main
			class="main"
			transition:fly={{ duration: 500, easing: quadInOut, x: 0, y: '20%', opacity: 0 }}
		>
			<div class="subheading">
				<h2 class="h2">
					<div
						class="generated"
						bind:this={GeneratedWrapper}
						style={`transition-duration: 250ms; transform: rotate(${genTextRotation}); opacity: ${genTextOpacity};`}
					>
						<span class="text">{generatedText}</span>
					</div>
					<span>by you</span>
				</h2>
			</div>
			<!-- div.SubMainHeading -->
			
			<div class="cta">
				<button class="button" on:click={toggleGenerated}>
					<span>Cycle</span>
				</button>
			</div>
			<!-- div.CTA -->
		</main>
	{/if}

	{#if showPage}
		<footer class="footer" transition:scale={{ delay: 500, duration: 500, easing: quintInOut, start: 0, opacity: 0 }}>
			<span>
				Crafted at The Webware Workshop
			</span>
		</footer>
	{/if}
</div>

<style>
	.container {
		width: 100%;
		max-width: 900px;
		height: 100%;
		overflow-y: auto;
		position: relative;
	}

	.about-container {
		padding: 20px;
		position: fixed;
		top: 0;
		right: 0;

		& > .button {
			color: hsl(var(--clr-black-bean));
			padding: 12px;
			background: hsl(var(--clr-pale-dogwood));

			&:where(:hover, :focus) {
				color: hsl(var(--clr-pale-dogwood));
				background: hsl(var(--clr-black-bean));
			}
		}
	}

	.main {
		padding-top: 60px;
		padding-inline: 20px;
		padding-bottom: 60px;

		@media screen and (min-width: 900px) {
			padding-top: 120px;
		}

		& > .subheading {
			font-size: 40px;
			font-weight: 900;
			line-height: 1;
			color: hsl(var(--clr-pale-dogwood));
			max-width: 100%;

			@media screen and (min-width: 900px) {
				font-size: 60px;
			}

			& > .h2 {
				font: inherit;

				& > .generated {
					color: hsl(var(--clr-black-bean));
					transform-origin: left center;
					text-transform: capitalize;
					position: relative;

					&::selection {
						color: hsl(var(--clr-pale-dogwood));
						background: hsl(var(--clr-black-bean));
					}
				}
			}
		}

		& > .cta {
			padding-top: 60px;

			& > .button {
				color: hsl(var(--clr-black-bean));
				padding: 20px 60px;
				background: hsl(var(--clr-pale-dogwood));

				&:where(:hover, :focus) {
					color: hsl(var(--clr-pale-dogwood));
					background: hsl(var(--clr-black-bean));
				}
			}
		}
	}

	.footer {
		position: fixed;
		bottom: 0;
		right: 0;
		isolation: isolate;
		padding: 24px;

		& > span {
			color: hsl(var(--clr-black-bean));
		}

		& > .link {
			font-size: 16px;
			font-weight: 500;
			line-height: 1.5;
			color: hsl(var(--clr-black-bean));
			text-decoration: none;
			outline: 2px dashed transparent;
			outline-offset: 4px;

			&:hover {
				color: hsl(var(--clr-pale-dogwood));
			}

			&:focus-visible {
				outline-color: hsl(var(--clr-pale-dogwood));
			}
		}
	}
</style>
