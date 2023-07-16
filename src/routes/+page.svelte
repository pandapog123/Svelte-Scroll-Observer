<script>
  import { ScrollObserver } from "$lib/index.js";
  import { slide } from "svelte/transition";

  let section2showing = false;
</script>

<div class="fixed">
  Showing section two:
  <span class="bool">
    {section2showing}
  </span>
</div>

<section>
  <ScrollObserver>
    <h1>Section one</h1>
  </ScrollObserver>
</section>

<section>
  <ScrollObserver
    showOnce
    bind:showing={section2showing}
    transition={(element) => slide(element)}
  >
    <h1>Section two</h1>
  </ScrollObserver>
</section>

<section>
  <ScrollObserver>
    <h1>Section three</h1>
  </ScrollObserver>
</section>

<style>
  .fixed {
    position: fixed;
    left: 16px;
    top: 24px;
  }

  .bool {
    padding: 8px;
    background-color: cadetblue;
    border-radius: 4px;
    color: white;
  }

  section {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
