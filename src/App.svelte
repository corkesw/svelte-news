<script>
  import { Router, Link, Route } from "svelte-navigator";
  import Articles from "./components/Articles.svelte";
  import Header from "./components/Header.svelte";
  import Nav from "./components/Nav.svelte";
  import Login from "./components/Login.svelte";
  import { user } from "./stores";
  let topic;
  let sortBy = "title";
  let order = "asc";
  let page = 1;

  let userValue
  user.subscribe(value => {
    console.log(value)
    userValue = value
  })
  
</script>

<Router primary={false}>
  <Header />
  <Nav />

  <main>
    <Route path="/articles">
      <Articles bind:topic bind:sortBy bind:order bind:page />
    </Route>
    <Route path="/">
      <Articles bind:topic bind:sortBy bind:order bind:page />
    </Route>
    <Route path="articles/:chosenTopic" let:params>
      <Articles chosenTopic={params.chosenTopic} />
    </Route>
    <Route path="/login"><Login /></Route>
  </main>
</Router>

<style>
  /* main {
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
  } */
</style>
