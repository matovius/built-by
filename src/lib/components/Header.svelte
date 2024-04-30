<script lang="ts">
  /**
   * Describes whether the page is loaded
   */
  export let isPageLoaded: boolean = false;

  /**
   * The header element
   */
  let Header: HTMLElement;

  $: if (isPageLoaded && Header) {
    Header.style.transform = 'scale(50%)';
    Header.style.opacity = '0.2';
  }

  $: if (!isPageLoaded && Header) {
    Header.style.removeProperty('transform');
    Header.style.removeProperty('opacity');
  }
</script>

<header class="header" bind:this={Header}>
  <h1 class="heading">
    <span>Built</span>
    <br />
    <span>By</span>
  </h1>
</header>

<style>
	.header {
		width: 100%;
		padding-inline: 20px;
		padding-block: 20px;
		isolation: isolate;
    transform-origin: 0 0;

		& > .heading {
			font-size: 90px;
			font-weight: 900;
			line-height: 1;
			color: hsl(var(--clr-black-bean));

			@media screen and (min-width: 900px) {
				font-size: 180px;
			}
		}
	}
</style>
