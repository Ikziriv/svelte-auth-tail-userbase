<script>
  import Button from "../components/Button.svelte";
  import Input from "../components/Input.svelte";
  import { userBaseStore, userStore, promiseStore } from "../stores";

  export let username, email, password;

  function signup() {
    $promiseStore = $userBaseStore
      .signUp({ username, email, password })
      .then((user) => ($userStore = user));
  }
</script>

<div class="w-full h-auto py-16 px-0">
  <div
    class="flex max-w-sm mx-auto overflow-hidden bg-white rounded-lg shadow-lg dark:bg-gray-800 lg:max-w-4xl"
  >
    <div
      class="hidden bg-cover lg:block lg:w-1/2"
      style="background-image:url('https://images.unsplash.com/photo-1606660265514-358ebbadc80d?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1575&q=80')"
    />

    <div class="w-full px-6 py-8 md:px-8 lg:w-1/2">
      <form on:submit|preventDefault={signup}>
        <div class="mt-4">
          <label
            class="block mb-2 text-sm font-medium text-gray-600 dark:text-gray-200"
            for="LoggingEmailAddress">Username</label
          >
          <Input bind:value={username} type="username" />
        </div>

        <div class="mt-4">
          <label
            class="block mb-2 text-sm font-medium text-gray-600 dark:text-gray-200"
            for="LoggingEmailAddress">Email Address</label
          >
          <Input bind:value={email} type="email" />
        </div>

        <div class="mt-4">
          <div class="flex justify-between">
            <label
              class="block mb-2 text-sm font-medium text-gray-600 dark:text-gray-200"
              for="loggingPassword">Password</label
            >
            <a
              href="#"
              class="text-xs text-gray-500 dark:text-gray-300 hover:underline"
              >Forget Password?</a
            >
          </div>

          <Input bind:value={password} type="password" />
        </div>

        <div class="mt-8">
          <Button>Sign Up</Button>
        </div>
      </form>
    </div>
  </div>
</div>
