<script>
  import { onMount } from "svelte";

  import { getArticles } from "../utils/api";

  export let topic = "banana";
  export let sortBy = "title";
  export let order = "asc";
  export let page = "1";

  console.log(topic);

  onMount(
    getArticles(topic, sortBy, order, page)
      .then((res) => {
        console.log(res);
        console.log("component did mount");
      })
      .catch((err) => console.log(err))
  );
</script>

<div>
  <p>Articles</p>
</div>
