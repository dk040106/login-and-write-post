<script>
  import { createEventDispatcher } from "svelte";

  import Tabs from "../../shared/Tabs.svelte";
  import SignIn from "./SignIn.svelte";
  import CreateAccount from "./CreateAccount.svelte";

  let dispatch = createEventDispatcher();

  let users = [{ username: "a", password: "a" }];

  // tabs
  let items = ["Sign In", "Create Account"];
  let activeItem = "Sign In";
  const tabChangeHandler = event => (activeItem = event.detail);

  // users
  const handleCreateUser = event => {
    const user = event.detail;
    users = [user, ...users];
    activeItem = "Sign In";
  };

  const handleSignIn = event => {
    const userInput = event.detail;
    if (
      users.find(
        user =>
          user.username === userInput.username &&
          user.password === userInput.password
      )
    ) {
      dispatch("validUser", userInput.username);
    } else {
      alert("Invalid username or password");
    }
  };
</script>

<style>
  .main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

<div class="main">
  <Tabs {items} {activeItem} on:tabChange={tabChangeHandler} />
  {#if activeItem === 'Sign In'}
    <SignIn on:signIn={handleSignIn} />
  {:else if activeItem === 'Create Account'}
    <CreateAccount on:createUser={handleCreateUser} />
  {/if}
</div>
