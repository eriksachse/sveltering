<script>
  import Sveltering from "$lib/Sveltering.svelte";
  import { onMount } from "svelte";
  let container;
  onMount(() => {
    for (let child of container.childNodes) {
      // console.log(child.nodeName === "#text", child);
    }
  });
</script>

<Sveltering method="words" bind:container>
  <div>This sentence has been Svelteringed!</div>
  This as well!
  <div>This sentence has been Svelteringed as well!</div>
</Sveltering>
