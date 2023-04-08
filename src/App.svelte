<script>
  let todos = [{id: 5, label: 'cheese'}]
  let id = 0

  const addATodo = (e) => {
    let newTodoList = [...todos, {id: id++, label: e.target[0].value, isComplete: false, editMode: false}]
    todos = newTodoList
    e.target[0].value = ''
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
            <span>{todo.label}</span>
          </div>

          <div class="todo-buttons">
            <button>edit</button>
            <button>delete</button>
          </div>
        </li>
      {/each}
    </ul>
  </div>
</main>

<style>
 
</style>
