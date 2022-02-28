<script>
  import { onMount } from "svelte";

  import { Link } from "svelte-navigator";
  import { getTopics } from "../utils/api";

  let topics = [];

  export let topic;

  onMount(async () => {
    topics = await getTopics();
  });

  $: console.log(topic);
</script>

<nav class="nav">
  <Link to={`/articles`} on:click={(topic = undefined)}
    ><p class={`nav--link${topic === undefined}`}>home</p></Link
  >
  {#each topics as topicLink}
    <Link to={`/articles/${topicLink.slug}`} on:click={(topic = topicLink.slug)}
      ><p class={`nav--link${topic === topicLink.slug}`}>
        {topicLink.slug}
      </p></Link
    >
  {:else}
    <p>Loading...</p>
  {/each}
</nav>

<style>
  .nav {
    margin: 0vw 7.5vw;
    display: flex;
  }

  .nav--linktrue {
    padding: 0vw 5vw 0vw 0vw;
    color: white;
    font-weight: bold;
  }

  .nav--linkfalse {
    padding: 0vw 5vw 0vw 0vw;
    color: gold;
    font-weight: bold;
  }
</style>
