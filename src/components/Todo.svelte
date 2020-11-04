<script>

  export let todo;

  import { createEventDispatcher, tick } from 'svelte';
  import { selectOnFocus, focusOnLoad } from '../actions';
  const dispatch = createEventDispatcher();
  
  let editing = false;
  let name = todo.name;
  let nameEl;

  function update(updateTodo) {
    todo = {...todo, ...updateTodo}
    dispatch('update', todo)
  }

  function onCancel() {
    name = todo.name;
    editing = false;
  }

  async function onEdit() {
    editing = true;
    await tick();
    nameEl.focus();
  }

  function onRemove() {
    dispatch('remove', todo)
  }

  function onSave() {
    update({name});
    editing = false;
  }

  function onToggle() {
    update({ completed: !todo.completed})
  }

</script>

<div>
  {#if editing} 
  <form on:submit|preventDefault={onSave} on:keydown={e => e.key === 'Escape' && onCancel()}>
    <label for="todo-{todo.id}" class="todo-label">
      New name for {todo.name}
    </label>
    <input type="text" use:selectOnFocus use:focusOnLoad bind:this={nameEl} bind:value={name} id="todo-{todo.id}" autocomplete="off" autocapitalize="off" />
    <div>
      <button type="button" class="p-4" on:click={() => onSave()} disabled={!name}>
        Save<span class="hidden"> new name for {todo.name}</span>
      </button>
      <button type="button" class="p-4 bg-red-500" on:click={() => onCancel()}>
        Cancel<span class="hidden"> renaming {todo.name}</span>
      </button>
    </div>
  </form>
  {:else}
  <div>
    <input type="checkbox" id="todo-{todo.id}" checked={todo.completed} on:click={() => onToggle()}/>
    <label for="todo-{todo.id}" class="todo-label">
      {todo.name}
    </label>
  </div>
  <div>
    <button type="button" class="p-4" on:click={() => onEdit()}>
      Edit <span class="hidden">{todo.name}</span>
    </button>
    <button type="button" class="p-4 bg-red-500" on:click={() => onRemove()}>
      Delete <span class="hidden">{todo.name}</span>
    </button>
  </div>
  {/if}
</div>