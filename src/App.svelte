<script>
  let todos = [{id: 500000, label: 'cheese'}]
  let id = 0
  let value

  const addATodo = (e) => {
    let newTodoList = [...todos, {id: id++, label: e.target[0].value, isComplete: false, editMode: false}]
    todos = newTodoList
    e.target[0].value = ''
  }

  const editOrSave = (id) => {
    const updatedTodos = todos.map(todo => {
      if (todo.id === id) {
        return {id: todo.id, label: todo.label, isComplete: todo.isComplete, editMode: !todo.editMode}
      } else {
        return todo
      }
    })
    todos = updatedTodos
  }
  
</script>

<main>
  <div class="wrapper">
    <h1>TODO</h1>

    <form class="add-todos" on:submit|preventDefault={addATodo}>
      <input type="text" placeholder="Create a new todo...">
      <button type="submit">+</button>
    </form>

    <ul class="todo-list">
      {#each todos as todo}
        <li class="todo">
          <div class="todo-label">
            <input type="checkbox">
            {#if todo.editMode}
            <form on:submit|preventDefault={() => editOrSave(todo.id)}>
              <input type="text" bind:value={todo.label}>
            </form>
            {:else}
            <span>{todo.label}</span>
            {/if}
          </div>

          <div class="todo-buttons">
            <button on:click={() => editOrSave(todo.id)}>{todo.editMode ? 'save' : 'edit'}</button>
            <button>delete</button>
          </div>
        </li>
      {/each}
    </ul>
  </div>
</main>

<style>
 
</style>
