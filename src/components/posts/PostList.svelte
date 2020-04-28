<script>
  import PostDetails from "./PostDetails.svelte";

  export let posts = [];
</script>

<style>
  .post-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>

<div class="post-list">
  {#each posts as post (post.id)}
    <div>
      <PostDetails {post} />
    </div>
  {/each}
</div>
