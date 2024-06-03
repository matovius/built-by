<script lang="ts">
	import { onMount } from 'svelte';
	import { adjectives } from '$lib/adjectives';
	import { fly } from 'svelte/transition';
	import { quadInOut } from 'svelte/easing';

	let showPage: boolean = false;
	let generatedText: string = '';
	let isGenerated: boolean = false;
	

	function toggleGenerated() {
		
		isGenerated = false;
		setTimeout(() => {
			generatedText = getRandomAdjective();
			isGenerated = true;
		}, 250);
	}

	function getRandomAdjective(): string {
		let randomAdjective: string = adjectives[Math.floor(Math.random() * adjectives.length)];
		return randomAdjective;
	}

	onMount(() => {
		setTimeout(() => {
			generatedText = getRandomAdjective();
			isGenerated = true;
			showPage = true;
		}, 200);
	});
</script>

<svelte:head>
	<title>Built By</title>
</svelte:head>

{#if showPage}
	<div class="generator" transition:fly={{ duration: 200, easing: quadInOut, x: 0, y: "10%", opacity: 0 }}>
		<h2 class="heading">
			<div class="generated">
				{#if isGenerated}
					<span
						in:fly={{ duration: 200, easing: quadInOut, x: 40, y: 0, opacity: 0 }}
						out:fly={{ duration: 200, easing: quadInOut, x: -40, y: 0, opacity: 0 }}
					>{generatedText}</span>
				{/if}
			</div>
			<span>by you</span>
		</h2>
		
		<div class="cta">
			<button class="button" on:click={toggleGenerated}>
				<span>Generate</span>
			</button>
		</div>
		<!-- div.CTA -->
	</div>
{/if}

<style>
	.generator {
		width: 100%;
		max-width: 1200px;
		display: flex;
		flex-direction: column;
		gap: 60px;
		
		& > .heading {
			font-size: 40px;
			font-weight: 900;
			line-height: 1;
			color: hsl(var(--clr-pale-dogwood));
			display: flex;
			flex-direction: column;

			@media screen and (min-width: 600px) {
				font-size: 60px;
			}

			& > .generated {
				color: hsl(var(--clr-black-bean));
				text-transform: capitalize;
				width: 100%;
				height: 40px;

				&::selection {
					color: hsl(var(--clr-pale-dogwood));
					background: hsl(var(--clr-black-bean));
				}

				@media screen and (min-width: 600px) {
					height: 60px;
				}

				& > span {
					display: inline-block;
					width: 100%;
				}
			}
		}

		& > .cta {
			& > .button {
				color: hsl(var(--clr-black-bean));
				width: 100%;
				padding-inline: 90px;
				padding-block: 30px;
				background: hsl(var(--clr-pale-dogwood));

				&:where(:hover, :focus) {
					color: hsl(var(--clr-pale-dogwood));
					background: hsl(var(--clr-black-bean));
				}

				@media screen and (min-width: 480px) {
					max-width: max-content;
				}
			}
		}
	}
</style>
