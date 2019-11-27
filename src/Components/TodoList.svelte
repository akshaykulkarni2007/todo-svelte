<script>
  import TodoItem from "./TodoItem.svelte";

  export let todos;
</script>

<ul class="list-group">
  {#if todos.length === 0}
    <span>Nothing to display</span>
  {:else}
    {#each todos as todo}
      <TodoItem {todo} on:delete on:toggle />
    {/each}
  {/if}
</ul>
