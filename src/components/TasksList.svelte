<script lang="ts">
  import { createEventDispatcher } from "svelte";

  interface task {
    id: string;
    task: string;
    checked: boolean;
  }
  export let tasks: task[] = [];
  const dispatch = createEventDispatcher();

  function toggleChecked(id: string) {
    dispatch("toggledChecked", id);
  }

  function deleteTask(id: string) {
    dispatch("deletedTask", id);
  }
</script>

<ul>
  {#each tasks as task (task.id)}
    <li>
      <input
        type="checkbox"
        id={task.id}
        checked={task.checked}
        on:change={() => toggleChecked(task.id)}
      />
      <label for={task.id} class:checked={task.checked}>
        {task.task}
      </label>

      <button on:click={() => deleteTask(task.id)}>X</button>
    </li>
  {/each}
</ul>

<style>
  ::-webkit-scrollbar {
    width: 10px;
  }

  ::-webkit-scrollbar-track {
    background: #1a1a1a;
    border-radius: 9999px;
  }

  ::-webkit-scrollbar-thumb {
    background: #333;
    border-radius: 99px;
    &:hover {
      background-color: #555;
    }
  }

  ul {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    flex: 1 1 0;
    overflow-y: auto;
    padding-right: 0.5rem;
  }

  ul li {
    padding: 0.5rem 1rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    border-bottom: 1px solid #444;
    &:hover {
      background-color: #222;
    }
    & button {
      display: flex;
      align-items: center;
      justify-content: center;
      background: transparent;
      font-size: 1rem;
      font-weight: bold;
      width: 20px;
      height: 20px;
      padding: 1rem;
      color: #eee;
      border: 0;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.2s;
      &:hover {
        background-color: #ca342f;
      }
      &:active {
        filter: brightness(1.5);
      }
    }
  }
  ul li label {
    font-size: 1rem;
    font-family: "Poppins";
    flex: 1;

    &.checked {
      text-decoration: line-through;
    }
  }
</style>
