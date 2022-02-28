<script>
  import { getUsers } from "../utils/api";
  import { user } from "../stores";

  let err = false;
  let userInput = "";

  let userValue;
  user.subscribe((value) => {
    console.log(value);
    userValue = value;
  });

  $: console.log(userInput);

  const handleLogin = (e) => {
    err = null;
    getUsers(userInput).then((res) => {
      if (res) {
        user.update((user) => userInput);
        localStorage.setItem("loggedInUser", userInput);
        userInput = "";
      } else {
        err = "User not found";
        userInput = "";
      }
    });
  };

  const handleLogout = () => {
    localStorage.removeItem("loggedInUser");
    user.update((user) => "");
  };
</script>

{#if userValue}
  <p>You are logged in as {userValue}</p>
  <button on:click={handleLogout}>Logout</button>
{:else}
  <div class="login">
    <form class="loginform" on:submit|preventDefault={handleLogin}>
      <label for="username" name="username" />
      <input
        on:input={(e) => {
          // err = false;
          userInput = e.target.value;
        }}
        value={userInput}
        type="text"
        name="username"
        placeholder="username"
      />
      <button>Login</button>
      <br />
      {#if err}
        <p class="errormessage">{err}</p>
      {/if}
    </form>
    <span class="spacer" />
  </div>
{/if}
