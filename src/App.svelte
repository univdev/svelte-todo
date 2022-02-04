<script>
	import TodoItem from './components/TodoItem/index.svelte';
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
</style>

<div id="wrap">
	<div class="container">
		<h1 class="title">To Do!</h1>
		<ul class="todo-items">
			<li class="todo-item">
				<TodoItem
					title=제목
				/>
			</li>
		</ul>
	</div>
</div>