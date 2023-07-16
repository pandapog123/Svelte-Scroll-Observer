<script lang="ts">
  import { onMount } from "svelte";
  import type { TransitionConfig } from "svelte/transition";

  /**
   * Defaults to false.
   *
   * Is used to determine if the transition should only be applied to the component once.
   *
   * Usage:
   * ```svelte
   * <ScrollObserver showOnce>
   * ```
   */
  export let showOnce = false;

  /**
   * Provide a callback that returns a `TransitionConfig`.
   *
   * Usage:
   * ```svelte
   * <ScrollObserver
   *   transition={(element) => slide(element)}
   * >
   * ```
   */
  export let transition:
    | ((element: HTMLElement) => TransitionConfig)
    | undefined = undefined;

  /**
   * Used to bind a boolean value to see if the component is visible on the screen.
   *
   * Usage:
   * ```svelte
   * <ScrollObserver bind:showing={isSectionOneShowing}>
   * ```
   */
  export let showing: boolean = false;

  let showElement = false;
  let elementRef: HTMLElement | undefined;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      const observedElement = entries[0];

      showing = observedElement.isIntersecting;

      if (!showOnce) {
        showElement = observedElement.isIntersecting;

        return;
      }

      if (showElement || !observedElement.isIntersecting) {
        return;
      }

      showElement = true;
    });

    if (!elementRef) {
      return;
    }

    observer.observe(elementRef);
  });
</script>

<!--
  @component
  - Syntactic Sugar for the `IntersectionObserver` api.
  
  Usage:
  ```svelte
<ScrollObserver>

<ScrollObserver bind:showing={isSectionOneShowing}>

<ScrollObserver transition={(element) => slide(element)}>

<ScrollObserver showOnce>
  ```

-->
<div bind:this={elementRef}>
  {#if transition}
    {#if showElement}
      <div transition:transition class="animation-container">
        <slot />
      </div>
    {/if}
  {:else}
    <slot />
  {/if}
</div>
