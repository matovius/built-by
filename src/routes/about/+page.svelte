<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { quadInOut } from 'svelte/easing';

	let showPage: boolean = false;

	onMount(() => {
		setTimeout(() => {
			showPage = true;
		}, 200);
	});
</script>

<svelte:head>
	<title>About Built By</title>
</svelte:head>

{#if showPage}
  <div class="about" transition:fly={{ duration: 200, easing: quadInOut, x: 0, y: "10%", opacity: 0 }}>
    <h2 class="heading">About</h2>

    <p class="content">
      <span>
        Built By is for developers that are tired of always using the same adjective in the footers of all their projects.
        You'll get a suggestion from a curated list of adjectives, perfectly engineered for use in any project.
        Whichever one you fancy, you can use, no strings attached.
      </span>
      <br />
      <br />
      <span>
        Crafted at The Webware Workshop by Martin Matovu, Built By is completely free and open-source.
        Find the code on <a href="http://github.com/matovius/built-by" target="_blank" rel="noopener noreferrer" class="link">GitHub</a>.
      </span>
    </p>
    
    <div class="cta">
      <button class="button" on:click={() => { history.back() }}>
        <span>Go back</span>
      </button>
    </div>
    <!-- div.CTA -->
  </div>
{/if}

<style>
  .about {
    width: 100%;
    max-width: 1200px;
    display: flex;
    flex-direction: column;
    gap: 60px;
    
    & > .heading {
      font-size: 40px;
      font-weight: 900;
      line-height: 1;
      color: hsl(var(--clr-black-bean));

      @media screen and (min-width: 600px) {
        font-size: 60px;
      }
    }

    & > .content {
      font-size: 20px;
      line-height: 1.5;
      width: 100%;
      max-width: 600px;

      & .link {
        line-height: 1.5;
        color: hsl(var(--clr-pale-dogwood));
        text-decoration: none;
        padding-inline: 10px;
        padding-block: 5px;
        outline: 2px dashed transparent;
        outline-offset: 4px;
        position: relative;

        &::before {
          content: "";
          width: 100%;
          height: 2px;
          background: hsl(var(--clr-black-bean));
          position: absolute;
          bottom: 0;
          inset-inline: 0;
          z-index: -1;
        }

        &:is(:hover, :focus) {
          &::before {
            height: 100%;
            background: hsl(var(--clr-black-bean));
          }
        }
        &:focus-visible {
          outline-color: hsl(var(--clr-pale-dogwood));
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
