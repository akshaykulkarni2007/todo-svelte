<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let todo;
</script>

<li class="list-group-item d-flex justify-content-between align-items-center">
  <span>
    <input
      type="checkbox"
      class="mr-4"
      on:change={() => dispatch('toggle', todo.id)}
      checked={todo.completed ? 'checked' : ''} />
    {#if todo.completed}
      <del>{todo.title}</del>
    {:else}{todo.title}{/if}
  </span>
  <span
    class="badge badge-danger badge-pill"
    on:click={() => dispatch('delete', todo.id)}>
    X
  </span>
</li>

<!-- onChange={() => toggleComplete(item.id)}
					checked={item.completed ? "checked" : ""} 
                    
                    item.completed ? <del>{item.title}</del> :
                    
                    onClick={() => deleteTodo(item.id)} -->
