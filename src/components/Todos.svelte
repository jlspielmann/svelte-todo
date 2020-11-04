<script>
  import NewTodo from './NewTodo.svelte';
  import FilterButton from './FilterButton.svelte';
  import MoreActions from './MoreActions.svelte';
  import Todo from './Todo.svelte';
  export let todos = []

  $: totalTodos = todos.length
  $: completedTodos = todos.filter(todo => todo.completed).length

  function removeTodo(todo) {
    todos = todos.filter(t => t.id !== todo.id)
  }

  function addTodo(name) {
    todos = [...todos, {id: newTodoId, name: name, completed: false}];
  }

  function updateTodo(todo) {
    const i = todos.findIndex(t => t.id === todo.id)
    todos[i] = { ...todos[i], ...todo }
  }

  let newTodoId
  $: {
    if (totalTodos === 0) {
      newTodoId = 1;
    } else {
      newTodoId = Math.max(...todos.map(t => t.id)) + 1;
    }
  }

  let filter = 'all'
  const filterTodos = (filter, todos) => (
    filter === 'active' ? todos.filter(t => !t.completed) : 
    filter === 'completed' ? todos.filter(t => t.completed) : todos
  )

  function toggleAll(completed) {
    todos = todos.map(t => ({...t, completed }));
  }

  function removeCompleted() {
    todos = todos.filter(t => !t.completed)
  }
  
</script>


<!-- Todos.svelte -->
<div class="w-full max-w-lg px-4 mx-auto">
  <NewTodo on:addTodo={e => addTodo(e.detail)} autofocus />

  <FilterButton bind:filter on:remove={e => removeTodo(e.detail)} />

  <!-- TodosStatus -->
  <h2 id="list-heading">{completedTodos} out of {totalTodos} items completed</h2>

  <!-- Todos -->
 <ul>
   {#each filterTodos(filter, todos) as todo (todo.id)}
    <li>
      <Todo todo={todo} 
        on:update={e => updateTodo(e.detail)}
        on:remove={e => removeTodo(e.detail)} />
    </li>
   {:else}
      Nothing to do here!
   {/each}
 </ul>

  <hr class="mt-4 mb-4 border-black" />

  <MoreActions todos={todos}
    on:checkAll={e => toggleAll(e.detail)}
    on:removeCompleted={e => removeCompleted()}
      />
</div>