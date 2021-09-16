<script>
  export let label;
  export let value;
</script>

<div class="w-full mt-4">
  <input
    bind:value
    id={label}
    name={label}
    {...$$restProps}
    class="block w-full px-4 py-2 mt-2 text-gray-700 placeholder-gray-500 bg-white border border-gray-300 rounded-md dark:bg-gray-800 dark:border-gray-600 dark:placeholder-gray-400 focus:border-blue-500 dark:focus:border-blue-500 focus:outline-none focus:ring"
  />
</div>
