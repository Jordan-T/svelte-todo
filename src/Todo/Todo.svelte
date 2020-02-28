<script>
  import TodoItem from './TodoItem.svelte';

  let todos = [];

  let filter = 'all'; // 'all' | 'active' | 'completed'

  $: hasDone = todos.filter(todo => todo.done).length !== 0;
  $: notDoneTodos = todos.filter(todo => !todo.done);
  $: filteredTodo = filter === 'all' ? todos : filter === 'active' ? notDoneTodos : todos.filter(todo => todo.done)
  $: allChecked = notDoneTodos.length === 0

  function addTodo(text) {
    const newTodo = {
      id: Math.random().toString(),
      title: text,
      done: false,
    }
    todos = [newTodo, ...todos];
  }

  function editTodo(id, event) {
    todos = todos.map(todo => {
      if (todo.id === id) {
        return {
          ...todo,
          ...event.detail,
        }
      }
      return todo;
    });
  }

  function handleNewKeyup(event) {
      if(event.key === "Enter"){
        addTodo(event.target.value);
        event.target.value = '';
      }
  }
  function toggleCheckAll() {
    let done = !allChecked;

    todos = todos.map(todo => ({
      ...todo,
      done,
    }));
  }
  function deleteTodo(id) {
    todos = todos.filter(todo => todo.id !== id);
  }
  function clearCompleted() {
    todos = todos.filter(todo => todo.done !== true);
  }
</script>

<section class="todoapp">
  <header class="header">
    <h1>todos</h1>
    <input class="new-todo" placeholder="What needs to be done?" on:keyup={handleNewKeyup}>
  </header>
  {#if filteredTodo.length !== 0}
    <section class="main" style="display: block;">
      <input id="toggle-all" class="toggle-all" type="checkbox" on:click={toggleCheckAll} checked={allChecked}>
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        {#each filteredTodo as todo (todo.id)}
          <TodoItem
            todo={todo}
            on:edit={(data) => editTodo(todo.id, data)}
            on:delete={() => deleteTodo(todo.id)}
          />
        {/each}
      </ul>
    </section>
  {/if}
  <footer class="footer" style="display: block;">
    {#if notDoneTodos.length !== 0}
      <span class="todo-count"><strong>{notDoneTodos.length}</strong> items left</span>
    {/if}
    <ul class="filters">
      <li>
        <a href="#/" class:selected={filter === 'all'} on:click|preventDefault={() => filter = 'all'}>All</a>
      </li>
      <li>
        <a href="#/active" class:selected={filter === 'active'} on:click|preventDefault={() => filter = 'active'}>Active</a>
      </li>
      <li>
        <a href="#/completed" class:selected={filter === 'completed'} on:click|preventDefault={() => filter = 'completed'}>Completed</a>
      </li>
    </ul>
    {#if hasDone}
      <button class="clear-completed" style="display: block;" on:click={clearCompleted}>Clear completed</button>
    {/if}
  </footer>
</section>

<footer class="info">
  <p>Double-click to edit a todo</p>
  <p>Written by <a href="http://jordan.taisne.free.fr">Jordan-T</a></p>
  <p>Part of <a href="http://todomvc.com">TodoMVC</a> (not yet)</p>
</footer>
