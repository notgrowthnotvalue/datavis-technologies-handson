<script>
  let current = "";
</script>

<style>
  .active{
    background-color: #4CAF50;
  }
</style>

<!-- We will cover buttons later on! -->
<button class="btn btn-secondary {current == 'messi' ? 'active' : ''}" on:click={() => (current = "messi")}>
  Messi
</button>

<button class="btn btn-secondary {current == 'ronaldo' ? 'active' : ''}" on:click={() => (current = "ronaldo")}>
  Ronaldo
</button>

<button class="btn btn-secondary {current == 'neymar' ? 'active' : ''}" on:click={() => (current = "neymar")}>
  Neymar
</button>
