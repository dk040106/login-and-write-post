<script>
  import { createEventDispatcher } from "svelte";
  import Card from "../../shared/Card.svelte";
  export let post;

  const dispatch = createEventDispatcher();
</script>

<style>
  h3 {
    margin: 0 auto;
    color: #555;
  }
  p.subtitle {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 20px;
  }
  p.content {
    margin: 10px auto;
    line-height: 25px;
  }
</style>

<Card>
  <div class="post">
    <h3>{post.title}</h3>
    <p class="subtitle">{post.subtitle}</p>
    <p class="content">{post.content}</p>
  </div>
</Card>
