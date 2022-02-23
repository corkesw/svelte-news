<script>
  import Articles from "./components/Articles.svelte";
  let topic = "coding";
  let sortBy = "title";
  let order = "asc";
  let page = "1";
</script>

<main>
  <Articles bind:topic bind:sortBy bind:order bind:page />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
