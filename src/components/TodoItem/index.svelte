<script>
  import moment from 'moment';

  export let title = '';
  export let expired = new Date();
  export let workers = [];

  const getDateFormat = (date) => moment(date).format('YYYY-MM-DD');
</script>

<style>
  .todo-item {
    border: 1px solid #EEE;
    background-color: white;
    box-shadow: 0 0 5px rgba(0, 0, 0, .4);
    padding: 16px;
    border-radius: 8px;
  }
  .todo-item__title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 16px;
  }
  .todo-item__options {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .todo-item__worker {
    font-size: 14px;
  }
  .todo-item__expired {
    font-size: 14px;
    color: #AAA;
  }
</style>

<div class="todo-item">
  <div class="todo-item__title">{title}</div>
  <div class="todo-item__options">
    <div class="todo-item__worker">
      {#if workers.length <= 0}
        <span>할당 된 작업자가 없습니다.</span>
      {/if}
      {#each workers as { name }, index}
        <div class="todo-item__worker__item">
          { index + 1 }: { name }
        </div>
      {/each}
    </div>
    <div class="todo-item__expired">{getDateFormat(expired)}</div>
  </div>
</div>