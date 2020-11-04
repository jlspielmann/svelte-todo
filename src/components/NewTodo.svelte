<script>
  import { createEventDispatcher, onMount } from 'svelte';
  import { selectOnFocus } from '../actions';
  const dispatch = createEventDispatcher();

  export let autofocus = false;

  onMount(() => {
    if (autofocus) nameEl.focus();
  })

  let name = '';
  let nameEl;

  function addTodo() {
    dispatch("addTodo", name);
    name = '';
    nameEl.focus();
  }

  function onCancel() {
    name = '';
  }

</script>

  <!-- NewTodo -->
  <form class="flex flex-col" on:submit|preventDefault={addTodo}  on:keydown={e => e.key === 'Escape' && onCancel()}>
    <h2 class="p-4">
      <label for="todo-0">
        What needs to be done?
      </label>
    </h2>
    <input type="text" id="todo-0" bind:this={nameEl} use:selectOnFocus bind:value={name} autocomplete="off" class="h-12 border-black" />
    <button type="submit" disabled={!name} class="p-4 text-white bg-black">
      Add
    </button>
  </form>