  <script>
    export let filter = 'all'
  </script>
  
  <!-- Filter -->
  <div class="flex flex-row items-center w-11/12 pt-5 justify-self-center">
    <button aria-pressed={filter === 'all'} class="flex-1" class:text-white={filter==='all'} class:bg-black={filter==='all'} on:click={() => filter = 'all'}>
      <span class="hidden">Show</span>
      <span>All</span>
      <span class="hidden">tasks</span>
    </button>
    <button aria-pressed={filter === 'active'} class="flex-1"  class:text-white={filter==='active'} class:bg-black={filter==='active'} on:click={() => filter = 'active'}>
      <span class="hidden">Show</span>
      <span>Active</span>
      <span class="hidden">tasks</span>
    </button>
    <button aria-pressed={filter === 'completed'} class="flex-1" class:text-white={filter==='completed'} class:bg-black={filter==='completed'} on:click={() => filter = 'completed'}>
      <span class="hidden">Show</span>
      <span>Completed</span>
      <span class="hidden">tasks</span>
    </button>
  </div>