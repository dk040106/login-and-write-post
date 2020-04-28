<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../../shared/Button.svelte";

  let dispatch = createEventDispatcher();

  let fields = { username: "", password: "" };
  let errors = { username: "", password: "" };

  let valid = false;

  const submitHandler = () => {
    valid = true;

    // validate username
    if (fields.username.trim().length < 1) {
      valid = false;
      errors.username = "username cannot be empty";
    } else {
      errors.username = "";
    }

    // validate password
    if (fields.password.trim().length < 1) {
      valid = false;
      errors.password = "password cannot be empty";
    } else {
      errors.password = "";
    }

    // sign in
    if (valid) {
      let user = {
        ...fields
      };
      dispatch("signIn", user);
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
    <label for="username">Username</label>
    <input type="text" id="username" bind:value={fields.username} />
    <div class="error">{errors.username}</div>
  </div>
  <div class="form-field">
    <label for="password">Password</label>
    <input type="password" id="password" bind:value={fields.password} />
    <div class="error">{errors.password}</div>
  </div>
  <Button>Sign In</Button>
</form>
