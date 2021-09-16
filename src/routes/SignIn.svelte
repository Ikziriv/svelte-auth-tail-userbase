<script>
  import Button from "../components/Button.svelte";
  import Input from "../components/Input.svelte";
  import Link from "../components/Link.svelte";
  import { userBaseStore, userStore, promiseStore } from "../stores";

  export let username, password;

  function signin() {
    $promiseStore = $userBaseStore
      .signIn({ username, password })
      .then((user) => ($userStore = user));
  }
</script>

<div class="w-full h-auto py-16 px-0">
  <div
    class="w-full max-w-sm mx-auto overflow-hidden bg-white rounded-lg shadow-md dark:bg-gray-800"
  >
    <div class="px-6 py-4">
      <h3
        class="mt-1 text-xl font-medium text-center text-gray-600 dark:text-gray-200"
      >
        Welcome Back
      </h3>

      <p class="mt-1 text-center text-gray-500 dark:text-gray-400">
        Login or create account
      </p>

      <form on:submit|preventDefault={signin}>
        <div class="w-full mt-4">
          <Input bind:value={username} type="username" />
        </div>

        <div class="w-full mt-4">
          <Input bind:value={password} type="password" />
        </div>

        <div class="flex items-center justify-between mt-4">
          <Link
            href="/#/forget-password"
            class="text-sm text-gray-600 dark:text-gray-200 hover:text-gray-500"
            >Forget Password?</Link
          >

          <Button>Login</Button>
        </div>
      </form>
    </div>

    <div
      class="flex items-center justify-center py-4 text-center bg-gray-100 dark:bg-gray-700"
    >
      <span class="text-sm text-gray-600 dark:text-gray-200"
        >Don't have an account?
      </span>

      <Link
        href="/#/signup"
        class="mx-2 text-sm font-bold text-blue-600 dark:text-blue-400 hover:text-blue-500"
        >Register</Link
      >
    </div>
  </div>
</div>
