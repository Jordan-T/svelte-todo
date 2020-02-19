<script>
</script>

<section class="todoapp">
  <header class="header">
    <h1>todos</h1>
    <input class="new-todo" placeholder="What needs to be done?">
  </header>
  <section class="main" style="display: block;">
    <input id="toggle-all" class="toggle-all" type="checkbox">
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <li class="completed">
        <div class="view">
          <input class="toggle" type="checkbox">
          <label>todo 1</label>
          <button class="destroy"></button>
        </div>
      </li>
      <li class="">
        <div class="view">
          <input class="toggle" type="checkbox">
          <label>todo 2</label>
          <button class="destroy"></button>
        </div>
      </li>
      <li class="editing">
        <div class="view">
          <input class="toggle" type="checkbox">
          <label>todo 3</label>
          <button class="destroy"></button>
        </div>
        <input type="text" class="edit" value="todo 3" />
      </li>
    </ul>
  </section>
  <footer class="footer" style="display: block;">
    <span class="todo-count"><strong>4</strong> items left</span>
    <ul class="filters">
      <li>
        <a href="#/" class="selected">All</a>
      </li>
      <li>
        <a href="#/active">Active</a>
      </li>
      <li>
        <a href="#/completed">Completed</a>
      </li>
    </ul>
    <button class="clear-completed" style="display: block;">Clear completed</button>
  </footer>
</section>

<footer class="info">
  <p>Double-click to edit a todo</p>
  <p>Written by <a href="http://jordan.taisne.free.fr">Jordan-T</a></p>
  <p>Part of <a href="http://todomvc.com">TodoMVC</a> (not yet)</p>
</footer>
