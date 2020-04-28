<script>
  import CreatePostForm from "./CreatePostForm.svelte";
  import PostList from "./PostList.svelte";
  import UserMenu from "./UserMenu.svelte";
  import Tabs from "../../shared/Tabs.svelte";

  export let userName;

  // tabs
  let items = ["Posts", "Add Post"];
  let activeItem = "Posts";
  const tabChangeHandler = event => (activeItem = event.detail);

  // posts
  let posts = [
    {
      id: parseInt(Math.random() * 1000),
      title: "Python or JavaScript?",
      subtitle: "Python",
      content:
        "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum."
    },
    {
      id: parseInt(Math.random() * 1000),
      title: "Lorem",
      subtitle: "Lorem",
      content:
        "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum."
    }
  ];

  const handlePostAdd = event => {
    const post = event.detail;
    posts = [post, ...posts];
    activeItem = "Posts";
  };
</script>

<style>
  .main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

<div class="main">
  <UserMenu {userName} on:signOut />
  <Tabs {items} {activeItem} on:tabChange={tabChangeHandler} />
  {#if activeItem === 'Posts'}
    <PostList {posts} />
  {:else if activeItem === 'Add Post'}
    <CreatePostForm on:postAdd={handlePostAdd} />
  {/if}
</div>
