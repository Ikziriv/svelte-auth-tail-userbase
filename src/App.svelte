<script>
  import Router from "svelte-spa-router";
  import Tailwindcss from "./Tailwindcss.svelte";
  import ForgetPassword from "./routes/ForgetPassword.svelte";
  import SignIn from "./routes/SignIn.svelte";
  import SignUp from "./routes/SignUp.svelte";
  import Welcome from "./routes/Welcome.svelte";
  import Navbar from "./components/Navbar.svelte";
  import Footer from "./components/Footer.svelte";

  import { userBaseStore, userStore, promiseStore } from "./stores";

  const userbase = window.userbase;
  window.userbase = null;
  //   Stores
  $userBaseStore = userbase;
  $userStore = null;

  $promiseStore = userbase
    .init({ appId: "0c6c0e3f-d786-48fc-8624-6c3c19851518" })
    .then((session) => ($userStore = session.user));

  function signout() {
    $promiseStore = $userBaseStore.signOut().then(() => ($userStore = null));
  }
</script>

<Tailwindcss />

<div class="bg-white dark:bg-gray-800 w-full h-auto">
  <Navbar />
  {#await $promiseStore.then(() => Promise.reject())}
    loading
  {:catch error}
    {#if error}
      <strong>Error! {error}</strong>
    {/if}

    {#if $userStore}
      <div class="w-full text-white bg-blue-500">
        <div
          class="container flex items-center justify-between px-6 py-4 mx-auto"
        >
          <div class="flex">
            <svg viewBox="0 0 40 40" class="w-6 h-6 fill-current">
              <path
                d="M20 3.33331C10.8 3.33331 3.33337 10.8 3.33337 20C3.33337 29.2 10.8 36.6666 20 36.6666C29.2 36.6666 36.6667 29.2 36.6667 20C36.6667 10.8 29.2 3.33331 20 3.33331ZM21.6667 28.3333H18.3334V25H21.6667V28.3333ZM21.6667 21.6666H18.3334V11.6666H21.6667V21.6666Z"
              />
            </svg>

            <p class="mx-3">Hello, {$userStore.username}!</p>
          </div>

          <button
            on:click={signout}
            class="p-1 transition-colors duration-200 transform rounded-md hover:bg-opacity-25 hover:bg-gray-600 focus:outline-none"
            >Logout
          </button>
        </div>
      </div>
    {:else}
      <Router
        routes={{
          "/": Welcome,
          "/forget-password": ForgetPassword,
          "/signin": SignIn,
          "/signup": SignUp,
        }}
      />
    {/if}
  {/await}
  <Footer />
</div>

<style>
</style>
