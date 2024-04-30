<script lang="ts">
	import { quadInOut } from "svelte/easing";
	import { fly } from "svelte/transition";

	export let isOpen: boolean = false;

	let Modal: HTMLDialogElement;
	let opacity: number = 0;

	$: if (Modal && isOpen) {
		Modal.showModal();
		opacity = 1;
	}

	$: if (Modal && !isOpen) {
		opacity = 0;
		setTimeout(() => {
			Modal.close();
		}, 750);
	}
</script>

<dialog class="modal" bind:this={Modal}>
	<div class="container" style={`transition: opacity 250ms ease; opacity: ${opacity};`}>
		<div class="close-modal">
			<button
			class="button"
			on:click={() => {
				isOpen = false;
			}}
				>
				<span>Close</span>
			</button>
		</div>
		
		{#if isOpen}
			<div class="content" transition:fly={{ delay: 250, duration: 500, easing: quadInOut, x: 0, y: '10%', opacity: 0 }}>
				<h2 class="h2">Sophisticated adjectives for sophisticated developers</h2>
				<p class="p">
					Built By is for developers that are tired of always using the same adjective in the footers
					of all their projects. You'll get a suggestion from a curated list of adjectives, perfectly
					crafted for use in any project. Whichever one you fancy, you can use, no strings attached.
				</p>
			</div>
			<div class="backdrop"></div>
		{/if}
	</div>
</dialog>

<style>
	.modal {
		width: 0;
		height: 0;
		overflow: visible;
		margin: 0;
		padding: 0;
		border: none;
		transition-duration: 250ms;

		&::backdrop {
			background: transparent;
		}

		& > .container {
			isolation: isolate;
			width: 100dvw;
			height: 100dvh;
			display: flex;
			justify-content: center;
			align-items: center;
			position: fixed;
			inset: 0;

			& > .content {
				width: 100%;
				max-width: 900px;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
				gap: 40px;
				padding: 20px;

				& > .h2 {
					font-weight: 900;
					font-size: 40px;
					color: hsl(var(--clr-pale-dogwood));
					line-height: 1;

					@media screen and (min-width: 900px) {
						font-size: 60px;
					}
				}

				& > .p {
					font-size: 20px;
					color: hsl(var(--clr-white));
					line-height: 1.5;
				}
			}

			& > .close-modal {
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

			& > .backdrop {
				width: 100%;
				height: 100%;
				background: hsl(var(--clr-burnt-sienna));
				position: absolute;
				inset: 0;
				z-index: -1;
			}
		}
	}
</style>
