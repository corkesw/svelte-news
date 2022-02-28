<script>
  import { user } from "../stores";
  import {Link} from "svelte-navigator"
  let userValue;
  user.subscribe((value) => {
    console.log(value);
    userValue = value;
  });
</script>

<div>
  <header>
    <h1>Svelty News</h1>
    {#if userValue}
    <Link to="/login">
    <p>Hey {userValue}!</p>
    </Link>
    {/if}
  </header>
</div>
