<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { v4 } from "uuid";
  let text = "";

  let dispatch = createEventDispatcher();

  function addTask() {
    const newTask = {
      id: v4(),
      task: text,
      checked: false,
    };
    dispatch("taskAdded", newTask);
    text = "";
  }
</script>

<div>
  <button on:click={addTask} disabled={text.trim().length === 0}>Add</button>
  <input type="text" placeholder="Write a new task" bind:value={text} />
</div>

<style>
  div {
    width: 100%;
    display: flex;
    gap: 0.5rem;
  }
  input,
  button {
    padding: 0.75rem 1rem;
    font-size: 1rem;
    border-radius: 8px;
    border: 0;
    color: #eee;
  }
  input {
    flex: 1;
    background-color: #222;
    border: 1px solid #444;
  }
  button {
    background-color: #2aa030;
    color: #eee;
    font-weight: bold;
    cursor: pointer;
    transition: 0.2s;
    font-family: "Rubik";
    &:hover {
      filter: brightness(1.2);
    }
    &:disabled {
      filter: saturate(0.1);
      cursor: not-allowed;
    }
  }
</style>
