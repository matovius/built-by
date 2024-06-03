<script lang="ts">
	import Logo from "./Logo.svelte";
</script>

<header class="header">
  <div class="container">
    <div class="logo-wrapper">
      <Logo />
    </div>

    <nav class="nav">
      <a href="/about" class="link">About</a>
    </nav>
  </div>
</header>

<style>
	.header {
		width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
		padding-inline: 30px;
    background: hsl(var(--clr-burnt-sienna));
    position: sticky;
    top: 0;
    z-index: 10;

    & > .container {
      width: 100%;
      max-width: 1200px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-block: 30px;

      & > .logo-wrapper {
        width: 60px;
        height: 60px;
        aspect-ratio: 1;
      }

      & > .nav {
        font-size: 20px;
        font-weight: 600;
        
        & > .link {
          isolation: isolate;
          line-height: 1.5;
          color: hsl(var(--clr-black-bean));
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
            background: hsl(var(--clr-black-bean), 0.2);
            position: absolute;
            bottom: 0;
            inset-inline: 0;
            z-index: -1;
          }

          &:is(:hover, :focus) {
            color: hsl(var(--clr-pale-dogwood));
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
    }
	}
</style>
