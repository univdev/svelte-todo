<script>
  import { createEventDispatcher } from 'svelte';
  import Input from '../Input/index.svelte';

  export let title = '';
  export let workers = '';
  export let expired = null;
  export let visible = false;

  const dispatch = createEventDispatcher();

  const handleSubmit = () => {
    const splitedWorkers = workers.split(',').map((i) => i.trim());
    const payload = { title, workers: splitedWorkers, expired };
    dispatch('submit', payload);
    clearPayload();
  };
  const handleClosePopup = () => {
    dispatch('close');
    clearPayload();
  };
  const clearPayload = () => {
    title = '';
    workers = '';
    expired = null;
  };
  const handleChangeTitle = (e) => {
    title = e.detail;
  };
  const handleChangeWorkers = (e) => {
    workers = e.detail;
  };
  const handleChangeExpired = (e) => {
    expired = e.detail;
  };
</script>

<style>
  .todo-form {
    position: fixed;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .45);
    left: 0;
    top: 0;
    animation: fade forwards .6s;
  }
  .todo-form-container {
    background-color: white;
    border-radius: 6px;
    width: 350px;
    height: 350px;
    position: absolute;
    overflow: auto;
    right: 50%;
    top: 50%;
    transform: translate(50%, -50%);
    border-radius: 8px;
  }
  .todo-form__title {
    text-align: center;
    padding: 16px;
    margin-bottom: 16px;
  }
  .todo-form__row {
    padding: 0 16px;
  }
  .todo-form__row:not(:last-of-type) {
    margin-bottom: 8px;
  }
  .submit-button {
    padding: 16px;
    text-align: center;
    font-size: 18px;
    color: blue;
    width: 100%;
    font-weight: bold;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }
  @keyframes fade {
    from { opacity: 0; }
    to { opacity: 1; }
  }
</style>

{#if visible}
<div class="todo-form"
  on:click={handleClosePopup}
>
  <form
    class="todo-form-container"
    on:click|stopPropagation={null}
    on:submit|preventDefault={handleSubmit}
  >
    <h2 class="todo-form__title">할 일 추가</h2>
    <div class="todo-form__row">
      <Input
        bind:value={title}
        placeholder="이름"
        on:input={handleChangeTitle}
      />
    </div>
    <div class="todo-form__row">
      <Input
        bind:value={workers}
        placeholder="작성자 (콤마로 구분)"
        on:input={handleChangeWorkers}
      />
    </div>
    <div class="todo-form__row">
      <Input
        bind:value={expired}
        type="date"
        placeholder="만료일"
        on:input={handleChangeExpired}
      />
    </div>
    <button class="submit-button">
      추가하기
    </button>
  </form>
</div>
{/if}