<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../../shared/Button.svelte";

  let dispatch = createEventDispatcher();

  let fields = { username: "", password: "", passwordVal: "" };
  let errors = { username: "", password: "", passwordVal: "" };

  let valid = false;

  const submitHandler = () => {
    valid = true;

    // validate username
    if (fields.username.trim().length < 5) {
      valid = false;
      errors.username = "username must be at least 5 characters long";
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

    // validate passwordVal
    if (fields.passwordVal.trim() != fields.password.trim()) {
      valid = false;
      errors.passwordVal = "mismatch with password";
    } else {
      errors.passwordVal = "";
    }

    // add new post
    if (valid) {
      let user = {
        ...fields,
        id: parseInt(Math.random() * 1000)
      };
      dispatch("createUser", user);
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
  <div class="form-field">
    <label for="passwordVal">Password Check</label>
    <input type="password" id="passwordVal" bind:value={fields.passwordVal} />
    <div class="error">{errors.passwordVal}</div>
  </div>
  <Button type="secondary">Create Account</Button>
</form>
