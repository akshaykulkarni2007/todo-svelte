<script>
  import { onMount } from "svelte";
  // import uuid from "uuid";

  import Header from "./Components/Header.svelte";
  import AddTodoForm from "./Components/AddTodoForm.svelte";
  import Filter from "./Components/Filter.svelte";
  import TodoList from "./Components/TodoList.svelte";

  let todos = [];

  onMount(() => {
    todos = JSON.parse(localStorage.getItem("todos")) || [];
  });

  const addTodo = e => {
    if (e.keyCode === 13) {
      const newTodo = {
        id: Math.random().toString(),
        title: e.target.value,
        completed: false
      };
      todos = [newTodo, ...todos];
      localStorage.setItem("todos", JSON.stringify(todos));
      e.target.value = "";
    }
  };

  const toggleComplete = id => {
    todos = todos.map(todo => {
      if (todo.id === id) todo.completed = !todo.completed;
      return todo;
    });
    localStorage.setItem("todos", JSON.stringify(todos));
  };

  const deleteTodo = id => {
    todos = todos.filter(todo => todo.id !== id);
    localStorage.setItem("todos", JSON.stringify(todos));
  };

  const applyFilter = filterText => {
    todos = todos.filter(todo =>
      todo.title.toLowerCase().includes(filterText.toLowerCase())
    );
  };
</script>

<style>

</style>

<Header />
<div class="container my-4">
  <AddTodoForm on:keyup={e => addTodo(e)} />
  <h4 className="mb-2">TODO List</h4>
  <Filter on:keyup={e => applyFilter(e.target.value)} />
  <TodoList
    {todos}
    on:toggle={id => toggleComplete(id.detail)}
    on:delete={id => deleteTodo(id.detail)} />
</div>
