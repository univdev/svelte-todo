<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let type = 'text';
  export let placeholder = '';
  export let value = '';

  const handleInput = (e) => {
    const { value } = e.target;
    dispatch('input', value);
  };
</script>

<style>
  .basic-input {
    width: 100%;
    border: 1px solid #EEE;
    border-radius: 4px;
    background-color: white;
    padding: 12px 8px;
  }
</style>

<input
  {value}
  {type}
  {placeholder}
  class="basic-input"
  on:input={handleInput}
>