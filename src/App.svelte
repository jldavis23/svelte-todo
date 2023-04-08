<script>
  let todos = []
  let id = 0

  const addATodo = (e) => {
    todos = [...todos, {id: id++, label: e.target[0].value, isComplete: false, editMode: false}]
    e.target[0].value = ''
  }

  const editOrSave = (id) => {
    todos = todos.map(todo => {
      if (todo.id === id) {
        return {id: todo.id, label: todo.label, isComplete: todo.isComplete, editMode: !todo.editMode}
      } else {
        return todo
      }
    })
  }

  const checkTodo = (id) => {
    todos = todos.map(todo => {
      if (todo.id === id) {
        return {id: todo.id, label: todo.label, isComplete: !todo.isComplete, editMode: todo.editMode}
      } else {
        return todo
      }
    })
  }

  const deleteTodo = (id) => {
    todos = todos.filter((todo) => todo.id !== id)
  }

  const clearCompletedTodos = () => {
    todos = todos.filter(todo => !todo.isComplete)
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
      {#each todos as todo (todo.id)}
        <li class="todo">
          <div class="todo-label">
            <input type="checkbox" on:click={() => checkTodo(todo.id)}>
            {#if todo.editMode}
            <form on:submit|preventDefault={() => editOrSave(todo.id)}>
              <input type="text" bind:value={todo.label}>
            </form>
            {:else}
            <span class:completed={todo.isComplete}>{todo.label}</span>
            {/if}
          </div>

          <div class="todo-buttons">
            <button on:click={() => editOrSave(todo.id)}>{todo.editMode ? 'save' : 'edit'}</button>
            <button on:click={() => deleteTodo(todo.id)}>delete</button>
          </div>
        </li>
      {/each}
    </ul>

    <div class="info">
      <p>{todos.filter(todo => !todo.isComplete).length} items left</p>
      <button on:click={clearCompletedTodos}>Clear Completed</button>
    </div>
  </div>
</main>
