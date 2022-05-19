<script lang="ts">
  import { onMount } from 'svelte';
  import { fly } from 'svelte/transition'

  const display = (number: number) => (number >= 10 ? "" : "0") + number.toString()
  let mounted = false;
  let date = new Date();
  let currentDate = new Date();
  $: dateDifference = +date - +currentDate
  $: dateDifferenceDate = new Date(dateDifference)
  onMount(() => {
    date = new Date()
    date.setTime(date.getTime() + (29 * 60 * 60 * 1000))
    setInterval(() => { currentDate = new Date() }, 50)
  })
</script>


<div class="text-white flex items-center justify-center align-middle w-screen h-screen lg:text-7xl md:text-6xl sm:text-4xl xl:text-9xl">
  {#if (+currentDate - +date) < 0}
  <div
    transition:fly={{ y: -150 }} 
    class="drop-shadow-[0_5px_0px_rgba(255,255,255,0.45)]"
    style="transform: skewX(2deg) skewY(4deg) translateX(-25%) translateY(25%)"
  >
    <span>waiting</span><br/>
    <span>{display(dateDifferenceDate.getHours())}:{display(dateDifferenceDate.getMinutes())}:{display(dateDifferenceDate.getSeconds())}</span><br/>
  </div>
  {:else}
    {#if mounted}
      <h2>run</h2>
    {:else}
      <h2>...</h2>
    {/if}
  {/if}
</div>