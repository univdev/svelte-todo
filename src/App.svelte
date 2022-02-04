<script>
	import TodoItem from './components/TodoItem/index.svelte';
	import TodoForm from './components/TodoForm/index.svelte';

	let todoItems = [];
	let isVisiblePopup = false;

	const handleShowPopup = () => {
		isVisiblePopup = true;
	};
	const handleHidePopup = () => {
		isVisiblePopup = false;
	};
	const handleAddTodoItem = (todoItem) => {
		isVisiblePopup = false;
		todoItems = [...todoItems, todoItem.detail];
	};
</script>

<style>
	#wrap {
		height: 100%;
		background-color: #93E6EA;
	}
	.container {
		max-width: 500px;
		width: 100%;
		height: 100%;
		background-color: white;
		margin: auto;
	}
	.title {
		padding: 16px;
		text-align: center;
	}
	.todo-items {
		list-style: none;
		padding: 0 16px;
	}
	.todo-item:not(:first-of-type) {
		margin-top: 16px;
	}
	.todo-item-add-button {
		width: 100%;
		padding: 16px;
		border: none;
		color: black;
		background-color: transparent;
		font-weight: bold;
		cursor: pointer;
	}
	.no-item-warning {
		padding: 16px;
		text-align: center;
		color: #CCC;
	}
</style>

<div id="wrap">
	<div class="container">
		<h1 class="title">To Do!</h1>
		<ul class="todo-items">
			{#each todoItems as { title, workers, expired }}
				<li class="todo-item">
					<TodoItem
						class="todo-item-component"
						title={title}
						workers={workers}
						expired={expired}
					/>
				</li>
			{/each}
			{#if todoItems.length <= 0}
				<div class="no-item-warning">
					데이터가 없습니다.
				</div>
			{/if}
		</ul>
		<button
			class="todo-item-add-button"
			type="button"
			on:click={handleShowPopup}
		>
			할 일 추가
		</button>
	</div>
</div>

<TodoForm
	visible={isVisiblePopup}
	on:close={handleHidePopup}
	on:submit={handleAddTodoItem}
/>