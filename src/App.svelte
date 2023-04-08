<script>
  let todos = [{id: 5, label: 'cheese'}]
  
</script>

<main>
  <div class="wrapper">
    <h1>TODO</h1>

    <form class="add-todos">
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
