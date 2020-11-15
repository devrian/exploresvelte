<script>
  import { onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte'

  let description = ''
  $: characters = description.length
  $: words = description.split(' ').length

  $: if (characters > 10) {
    console.log(`-----------`)
    console.log(`Description: ${description}`)
  }

  function handleSubmit(event) {
    console.log('form submitted. thanks!')
    description = ''
  }

  onMount(() => {
    console.log('onMount')
  })
  onDestroy(() => {
    console.log('onDestroy')
  })
  beforeUpdate(() => {
    console.log('beforeUpdate')
  })
  afterUpdate(() => {
    console.log('afterUpdate')
  })
</script>

<style>
  div {
    margin-top: 1em;
    margin-bottom: 1em;
  }
</style>

<div class="form-group">
  <p>{description}</p>
  <form on:submit|preventDefault={handleSubmit}>
    <textarea bind:value={description} rows="7" />
    <button type="submit">Save</button>
  </form>
  <p>Characters count: {characters}</p>
  <p>Words count: {words}</p>
</div>