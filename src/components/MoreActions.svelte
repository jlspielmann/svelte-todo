<script>
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher();

  export let todos;

  $: completed = todos.reduce((c, t) => t.completed && c, true);

  const checkAll = () => {
    dispatch("checkAll", !completed);
  }

  const removeCompleted = () => {
    dispatch("removeCompleted");
  }

  $: completedTodosCount = todos.filter(t => t.completed).length
</script>

  <!-- MoreActions -->
  <div class="flex flex-row justify-evenly">
    <button disabled={todos.length === 0} type="button" class="p-2 text-white bg-black flex-shrink-1" on:click={checkAll}>{completed? "Uncheck" : "Check"} all</button>
    <button disabled={completedTodosCount === 0} type="button" class="p-2 text-white bg-black flex-shrink-1" on:click={removeCompleted}>Remove completed</button>
  </div>
