<script>
  import "../app.css";
  import Sveltering from "$lib/Sveltering.svelte";
  import { onMount } from "svelte";
  let container;
  onMount(() => {
    console.log(container);
    for (let child of container.children) {
      setTimeout(() => {
        child.style.display = "inline-block";
        child.style.transform =
          "translate(" +
          (Math.round(Math.random() * 20) * 2 - 20) +
          "px," +
          (Math.round(Math.random() * 20) * 2 - 20) +
          "px) rotate(" +
          (Math.round(Math.random() * 20) * 2 - 20) +
          "deg)";
      }, 200);
    }
  });
</script>

<div id="container">
  <Sveltering method="words">
    <div bind:this={container}>This sentence has been Svelteringed!</div>
  </Sveltering>
</div>
<div id="info">
  <a href="https://github.com/eriksachse/sveltering"
    >https://github.com/eriksachse/sveltering</a
  >
</div>

<style>
  #container {
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    height: 100%;
    font-size: 4vw;
    font-family: "Work Sans Bold";
  }
  #info {
    position: absolute;
    bottom: 0px;
    margin: 12px;
  }
</style>
