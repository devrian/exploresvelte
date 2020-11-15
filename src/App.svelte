<script>
  import { fade, fly } from 'svelte/transition'

  import EmojiDisplay from './EmojiDisplay.svelte'
  import EmojiDescription from './EmojiDescription.svelte'
  import Button from './Button.svelte'

  let isLoaded = false
  let currentEmoji = '😃'
  let mouse = { x: 0, y: 0 }
  const emojis = ['🤣', '😉', '🚀', '😍']

  function randomizeEmoji() {
    return emojis[Math.floor(Math.random() * emojis.length)]
  }

  function handleRandomButton() {
    currentEmoji = randomizeEmoji()
  }

  function handleMouseMove(event) {
    mouse.x = event.clientX
    mouse.y = event.clientY
  }

  setTimeout(() => {
    isLoaded = true
  }, 2500)
</script>

<style>
  div {
    margin: 2em;
  }
</style>

<svelte:head>
  <link href='/terminal.min.css' rel="stylesheet" />
</svelte:head>

<div class="container" on:mousemove="{handleMouseMove}">
  <p>The mouse position: {mouse.x} x {mouse.y}</p>
  <h1>Randomize Emoji</h1>

  <ul>
    {#each emojis  as emoji}
      <li>{emoji}</li>
    {/each}
  </ul>

  {#if isLoaded === true}
    <div in:fly={{ y: 200, duration: 2000 }} out:fade>
      <EmojiDisplay {currentEmoji} />
      <EmojiDescription />
      <Button title={'🔁 Randomize'} on:click={handleRandomButton} />
    </div>
  {:else}
    <h2>Loading ...</h2>
  {/if}

  <Button title={'Toggle'} on:click={() => isLoaded = !isLoaded } />
</div>