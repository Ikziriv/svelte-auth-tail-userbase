<script>
  import Button from "../components/Button.svelte";
  import Input from "../components/Input.svelte";
  import Link from "../components/Link.svelte";
  import { userBaseStore, promiseStore } from "../stores";

  export let username;

  function forgetPassword() {
    $promiseStore = $userBaseStore.forgetPassword({ username });
  }
</script>

<div class="w-full h-auto py-16 px-0">
  <div
    class="w-full max-w-sm mx-auto overflow-hidden bg-white rounded-lg shadow-md dark:bg-gray-800"
  >
    <div class="px-6 py-4">
      <form on:submit|preventDefault={forgetPassword}>
        <div class="w-full mt-4">
          <Input bind:value={username} type="username" />
        </div>

        <div class="flex items-center justify-between mt-4">
          <Button>Send Email</Button>
        </div>
      </form>
    </div>

    <div
      class="flex items-center justify-center py-4 text-center bg-gray-100 dark:bg-gray-700"
    >
      <span class="text-sm text-gray-600 dark:text-gray-200 mr-2"
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
