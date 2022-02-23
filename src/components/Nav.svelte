<script>
  import { onMount } from "svelte";

  import { Link } from "svelte-navigator";
  import { getTopics } from "../utils/api";

  let topicList;
  onMount(
    getTopics()
      .then((topics) => {
        topicList = topics;
      })
      .catch((err) => console.log(err))
  );
</script>

<nav>
  {#each topicList as topic}
    <Link to={`/articles/${topic.slug}`}>{topic.slug}</Link>
  {/each}
</nav>
