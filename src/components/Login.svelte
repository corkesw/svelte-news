<script>


</script>


<div className="login">
    <form className="loginform" onSubmit={handleLogin}>
      <label htmlFor="username" name="username"></label>
      <input
        onChange={(e) => {
          setErr(null);
          setUserInput(e.target.value);
        }}
        value={userInput}
        type="text"
        name="username"
        placeholder="username"
      >
      <button>Login</button>
      <br />
      {#if err}
      <p class="errormessage">{err}</p>
      {/if}
      {#if user}
      <p>You are logged in as {user}</p>
      {/if}
    </form>
    <span className="spacer"></span>
  </div>