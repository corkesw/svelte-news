<script>
  import { user } from "../stores";
  import { Link } from "svelte-navigator";
  let userValue;
  user.subscribe((value) => {
    console.log(value);
    userValue = value;
  });
</script>

<div>
  <header class="header">
    <h1>Svelty News</h1>
    {#if userValue}
      <Link to="/login">
        <p>Hey {userValue}!</p>
      </Link>
    {/if}
  </header>
</div>

<style>
  .header {
    /* background-color: #094074; */
    padding: 0px;
    margin: 0px;
    text-align: center;
    color: #fbfbfb;
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    margin: 0vw 7.5vw;
}

.headerbutton {
    justify-content: center;
    vertical-align: baseline;
    margin-top: 5px;
}

.title {
    padding: 0px;
    margin: 0px
}


</style>
