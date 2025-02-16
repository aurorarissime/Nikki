<script lang="ts">
  export let open: boolean;

  const EASING = `cubic-bezier(0.4, 0, 0.2, 1)`;
  $: lineTransition = open
    ? `top 150ms 25ms ${EASING}, transform 150ms 175ms ${EASING}`
    : `top 150ms 175ms ${EASING}, transform 150ms 25ms ${EASING}`;
</script>

<style>
  .hamburger {
    position: relative;
    cursor: pointer;
    height: 1rem;
    width: 1.5rem;
    outline: none !important;
  }

  .line {
    position: absolute;
    background: currentColor;
    width: 100%;
    height: var(--line-width, 2px);
    border-radius: var(--line-width, 2px);
  }

  .line--first {
    top: 0;
  }
  .line--middle {
    top: 50%;
  }
  .line--bottom {
    top: 100%;
  }

  .open .line {
    top: 50% !important;
  }
</style>

<button
  class="hamburger"
  class:open
  on:click
  on:keydown
  on:keypress
>
  <!-- svelte-ignore element_invalid_self_closing_tag -->
  <span
    class="line line--first"
    style="transition: {lineTransition}; {open
      ? 'transform: rotate(45deg)'
      : ''}"
  />
    <!-- svelte-ignore element_invalid_self_closing_tag -->
    <span
      class="line line--middle"
      style="transition: {lineTransition}; {open
        ? 'transform: rotate(45deg)'
        : ''}"
    />
  <!-- svelte-ignore element_invalid_self_closing_tag -->
  <span
    class="line line--bottom"
    style="transition: {lineTransition}; {open
      ? 'transform: rotate(-45deg)'
      : ''}"
  />
</button>