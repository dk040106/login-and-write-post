<script>
  import Header from "./components/layouts/Header.svelte";
  import Footer from "./components/layouts/Footer.svelte";
  import Posts from "./components/posts/Posts.svelte";
  import Auth from "./components/auth/Auth.svelte";

  // user / auth
  let isSignedIn = false;
  let userName = "";

  const handleValidUser = event => {
    userName = event.detail;
    isSignedIn = true;
  };

  const handleSignOut = () => {
    isSignedIn = false;
    userName = "";
  };
</script>

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

<Header />
<main>
  {#if isSignedIn}
    <Posts {userName} on:signOut={handleSignOut} />
  {:else}
    <Auth on:validUser={handleValidUser} />
  {/if}
</main>
<Footer />
