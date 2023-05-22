<script lang="ts">
  import { onMount } from "svelte";

  interface task {
    task: string;
    id: string;
    checked: boolean;
  }

  import Input from "./components/Input.svelte";
  import Stats from "./components/Stats.svelte";
  import TasksList from "./components/TasksList.svelte";

  let tasks: task[] = [
    { id: "1", task: "Walk the dog", checked: true },
    { id: "2", task: "Wash the dishes", checked: false },
    { id: "3", task: "Do the laundry", checked: false },
  ];

  onMount(() => {
    const stored = JSON.parse(localStorage.getItem("tasks"));

    if (!stored)
      tasks = [
        { id: "1", task: "Walk the dog", checked: true },
        { id: "2", task: "Wash the dishes", checked: false },
        { id: "3", task: "Do the laundry", checked: false },
      ];
    else {
      tasks = stored;
    }
  });

  function handleAddTask(e: CustomEvent) {
    tasks = [e.detail, ...tasks];
    localStorage.setItem("tasks", JSON.stringify(tasks));
  }

  function handleDeleteTask(e: CustomEvent) {
    tasks = tasks.filter((task) => task.id !== e.detail);
    localStorage.setItem("tasks", JSON.stringify(tasks));
  }

  function handleToggledChecked(e: CustomEvent) {
    const id = e.detail;

    tasks = tasks.map((task) => {
      if (task.id === id) {
        return { ...task, checked: !task.checked };
      } else {
        return task;
      }
    });
    localStorage.setItem("tasks", JSON.stringify(tasks));
  }
</script>

<main>
  <h1>Tasks</h1>
  <Input on:taskAdded={handleAddTask} />
  <TasksList
    {tasks}
    on:toggledChecked={handleToggledChecked}
    on:deletedTask={handleDeleteTask}
  />
  <Stats
    total={tasks.length}
    done={tasks.filter((task) => task.checked).length}
  />
</main>

<style>
  main {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    width: 100%;
    flex: 1;
  }
  main h1 {
    text-align: center;
    font-family: "Rubik";
  }
</style>
