<script>
	import Todo from './lib/Todo.svelte'

    let todos = []
	
	const deleteTask = (id) => {
		todos = todos.filter((todo) => todo.id != id)
	}

	const addNewTodo = (e) => {
		const todo = e.detail
		todos = [todo, ...todos]
		console.log(todo.completed)
	}	
</script>

<Todo on:addingNewTodo={addNewTodo} />

<main>
	{#each todos as todo (todo.id)}
		<div class="todo">
			<p>{todo.task}</p>
			<button on:click={deleteTask(todo.id)}>delete</button>
		</div>
	{/each}
</main>

<style lang="scss">
	.todo {
		display: flex;
		align-items: center;
		gap: 24px;
	}
</style>