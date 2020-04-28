<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../../shared/Button.svelte";

  let dispatch = createEventDispatcher();

  let fields = { title: "", subtitle: "", content: "" };
  let errors = { title: "", subtitle: "", content: "" };

  let valid = false;

  const submitHandler = () => {
    valid = true;

    // validate question
    if (fields.title.trim().length < 5) {
      valid = false;
      errors.title = "title must be at least 5 characters long";
    } else {
      errors.title = "";
    }

    // validate subtitle
    if (fields.subtitle.trim().length < 1) {
      valid = false;
      errors.subtitle = "Subtitle cannot be empty";
    } else {
      errors.subtitle = "";
    }

    // validate content
    if (fields.content.trim().length < 1) {
      valid = false;
      errors.content = "Content cannot be empty";
    } else {
      errors.content = "";
    }

    // add new post
    if (valid) {
      let post = {
        ...fields,
        id: parseInt(Math.random() * 1000)
      };
      dispatch("postAdd", post);
    } else {
      console.log(errors);
    }
  };
</script>

<style>
  form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
  }
  input {
    width: 100%;
    border-radius: 6px;
  }
  label {
    margin: 10px auto;
    text-align: left;
  }
  textarea {
    resize: vertical;
    width: 100%;
  }
  .form-field {
    margin: 18px auto;
  }
  .error {
    font-weight: bold;
    font-size: 14px;
    color: #d91b42;
  }
</style>

<form on:submit|preventDefault={submitHandler}>
  <div class="form-field">
    <label for="title">Post Title</label>
    <input type="text" id="title" bind:value={fields.title} />
    <div class="error">{errors.title}</div>
  </div>
  <div class="form-field">
    <label for="subtitle">Subtitle</label>
    <input type="text" id="subtitle" bind:value={fields.subtitle} />
    <div class="error">{errors.subtitle}</div>
  </div>
  <div class="form-field">
    <label for="content">Content</label>
    <textarea id="content" bind:value={fields.content} />
    <div class="error">{errors.content}</div>
  </div>
  <Button type="secondary">Add Post</Button>
</form>
