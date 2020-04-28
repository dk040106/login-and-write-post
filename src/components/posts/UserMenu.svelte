<script>
  import { createEventDispatcher } from "svelte";
  import Card from "../../shared/Card.svelte";
  import Button from "../../shared/Button.svelte";

  export let userName;

  const dispatch = createEventDispatcher();

  const handleSignOut = () => {
    dispatch("signOut");
  };
</script>

<style>
  h2 {
    margin: 10px;
  }
  .usermenu {
    text-align: center;
    margin: 30px;
  }
</style>

<div class="usermenu">
  <Card>
    <h2>Hello {userName}!</h2>
    <button on:click={handleSignOut}>Sign Out</button>
  </Card>
</div>
