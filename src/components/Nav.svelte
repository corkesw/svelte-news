<script>
  import { onMount } from "svelte";

  import { Link } from "svelte-navigator";
  import { getTopics } from "../utils/api";

  let topics = [];

  export let topic

  onMount(async () => {
    topics = await getTopics();
  });
</script>

<nav>
    <Link to={`/articles`} on:click={topic=undefined}>home</Link>
  {#each topics as topicLink}
    <Link to={`/articles/${topicLink.slug}`} on:click={topic=topicLink.slug}>{topicLink.slug}</Link>
  {:else}
    <p>Loading...</p>
  {/each}
  
</nav>
