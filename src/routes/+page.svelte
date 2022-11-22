<script>
  import Sveltering from "$lib/Sveltering.svelte";
  import { onMount } from "svelte";
  let container;
  onMount(() => {
    console.log(container);
  });
</script>

<Sveltering method="words" bind:container>
  <div>This sentence has been Svelteringed!</div>
</Sveltering>
