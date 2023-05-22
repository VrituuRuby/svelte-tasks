<script>
  export let total = 0;
  export let done = 0;
</script>

<footer>
  <p>
    {done}
    {done === 1 ? "task" : "tasks"} done out of {total}
  </p>
</footer>

<style>
  footer {
    display: flex;
    justify-content: center;
    & p {
      font-size: 1rem;
      text-align: center;
      border-radius: 999px;
      padding: 0.5rem;
      background-color: #222;
    }
  }
</style>
