<script>
  import { tick } from "svelte";
  import Row from "./lib/Row.svelte";
  
  let even = true;
  let length = 20;
  let binding = true;
  let delta = 0;

  $: numbers = Array.from({length}, (_, i) => i)
  $: render = numbers.filter(x => {
    if(even) {
      return x % 2 === 0
    } else {
      return x % 2 !== 0
    }
  })

  async function toggle(cb) {
    const start = performance.now()
    console.time('Time taken')
    cb()
    await tick()
    delta = performance.now() - start
    console.timeEnd('Time taken')
  }

  function toggleEven() {
    toggle(() => even = !even)
  }
  
  function toggleBinding() {
    toggle(() => binding = !binding)
  }
</script>

<section>
  <div class="left">
    <div>
      <p>
        Amount of items rendered: {length / 2}
      </p>
      <label>
        Range 0 -
        <input step="2" type="number" bind:value={length} />
      </label>
      <button on:click={toggleEven}>Toggle odd/even</button>
    </div>
    <button on:click={toggleBinding}>Is using bind:clientWidth : {binding}</button>
    <div>
      Delta: {delta}ms
    </div>
  </div>
  <div>
    {#each render as index (index)}
      <Row {index} {binding}/>
    {/each}
  </div>
</section>

<style>
  section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: flex-start;
    height: 100vh;
  }

  .left {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>