<script lang="ts">
	import { onMount } from 'svelte';
	import { adjectives } from '$lib/adjectives';
	import AboutModal from '$lib/components/AboutModal.svelte';

	let MainHeading: HTMLHeadingElement;
	//let MainContent: HTMLElement;
	let GeneratedWrapper: HTMLDivElement;
	let generatedText: string;

	let mainContentOpacity: number = 0;
	let genTextOpacity: number = 0;
	let genTextRotation: string = '-90deg';
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
			MainHeading.style.transform = 'scale(50%)';
			MainHeading.style.opacity = '20%';
			mainContentOpacity = 1;
			showGenerated();
		}, 2000);
	});
</script>

<svelte:head>
	<title>Built By</title>
</svelte:head>

<div class="container">
	<header class="header">
		<h1 class="heading" bind:this={MainHeading}>
			<span>Built</span>
			<br />
			<span>By</span>
		</h1>
	</header>

	<main
		class="main"
		style={`opacity: ${mainContentOpacity}; transition: opacity 250ms ease-in; transition-delay: 500ms;`}
	>
		<div class="about-cta">
			<button
				class="button"
				on:click={() => {
					isAboutModalOpen = true;
				}}
			>
				<span>About</span>
			</button>
		</div>
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

		<AboutModal bind:isOpen={isAboutModalOpen} />
	</main>

	<footer class="footer">
		<span>
			Crafted at The Webware Workshop
		</span>
	</footer>
</div>

<style>
	.container {
		width: 100%;
		max-width: 900px;
		height: 100%;
		overflow-y: auto;
		position: relative;
	}

	.header {
		width: 100%;
		padding-inline: 20px;
		padding-block: 20px;
		isolation: isolate;

		& > .heading {
			font-size: 90px;
			font-weight: 900;
			line-height: 1;
			color: hsl(var(--clr-black-bean));
			transform-origin: 0 0;
			transition: transform opacity 500ms ease-in;

			@media screen and (min-width: 900px) {
				font-size: 180px;
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

		& > .about-cta {
			padding: 20px;
			position: fixed;
			top: 0;
			right: 0;

			& > .button {
				color: hsl(var(--clr-black-bean));
				padding: 20px;
				background: hsl(var(--clr-pale-dogwood));

				&:where(:hover, :focus) {
					color: hsl(var(--clr-pale-dogwood));
					background: hsl(var(--clr-black-bean));
				}
			}
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
