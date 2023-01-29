<script>
  import { afterUpdate } from 'svelte';

  // This is an example of a 'Reactive Value' where the DOM is updated
  afterUpdate(() => {
    document.querySelector('.js-todo-input').focus();
  });
  
  // This is an example of 'Variables'
  let todoItems = [];
  // This is an example of 'Variables'
  let newTodo = '';
  
  function addTodo() {
    newTodo = newTodo.trim();
    // This is an example of 'Control Flow', a conditional
    if (!newTodo) return;
    
    // This is an example of 'Props', properties of an object
    const todo = {
        text: newTodo,
        checked: false,
        id: Date.now(),
    };
  
    todoItems = [...todoItems, todo];
    newTodo = '';
  }
  function toggleDone(id) {
    const index = todoItems.findIndex(item => item.id === Number(id));
    todoItems[index].checked = !todoItems[index].checked;
  }
  function deleteTodo(id) {
    todoItems = todoItems.filter(item => item.id !== Number(id));
  }
  </script>

<main>
  <!-- The classes are examples of 'Reusable Components' -->
  <div class="container">
    <h1 class="app-title">todos</h1>
    <!-- This is an example of 'Control Flow' - a loop through items -->
    <ul class="todo-list">
      {#each todoItems as todo (todo.id)}
       <!-- This is an example of 'Control Flow' - a conditional check -->
        <li class="todo-item {todo.checked ? 'done' : ''}">
          <input id={todo.id} type="checkbox" />
          <label for={todo.id} class="tick" on:click={() => toggleDone(todo.id)}></label>
          <span>{todo.text}</span>
          <!-- This is an example of a 'Reactive Value' where the DOM is updated -->
          <button class="delete-todo" on:click={() => deleteTodo(todo.id)}>
            <svg><use href="#delete-icon"></use></svg>
          </button>
        </li>
      {/each}
    </ul>
    <div class="empty-state">
      <svg class="checklist-icon"><use href="#checklist-icon"></use></svg>
      <h2 class="empty-state__title">Add your first todo</h2>
      <p class="empty-state__description">What do you want to get done today?</p>
    </div>
    <!-- This is an example of a 'Reactive Value' where the DOM is updated -->
    <form on:submit|preventDefault={addTodo}>
      <!-- This is an example of a 'Binding' -->
      <input class="js-todo-input" type="text" aria-label="Enter a new todo item" placeholder="E.g. Build a web app" bind:value={newTodo}>
    </form>
  </div>
</main>
