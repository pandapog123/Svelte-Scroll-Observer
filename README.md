# Svelte Scroll Observer

### - Syntactic Sugar for the `IntersectionObserver` api.

### - Compatable with `SvelteKit`.

### Usage:

```svelte
<ScrollObserver>

<ScrollObserver bind:showing={isSectionOneShowing}>

<ScrollObserver transition={(element) => slide(element)}>

<ScrollObserver showOnce transition={(element) => fade(element)}>
```
