<script>
	import Todo from './lib/Todo.svelte'

    let todos = []
	
	const addNewTodo = (e) => {
		const todo = e.detail
		todos = [todo, ...todos]
	}	

	const deleteTask = (id) => {
		todos = todos.filter((todo) => todo.id != id)
	}
</script>


<main>
	<Todo on:addingNewTodo={addNewTodo} />
	{#each todos as todo (todo.id)}
		<div class="todo">
			<button 
			on:click={deleteTask(todo.id)}
			class="deleteBtn"
			>
				Delete
			</button>
			<p class={todo.completed ? 'completed' : 'notComplete'}>{todo.task}</p>
			<button 
			on:click={(() => todo.completed = !todo.completed)}
			class="completeBtn"
			>
				complete</button>
		</div>
	{/each}
</main>

<style lang="scss">
	main {
		margin-inline: auto;
		width: min(calc(100% - 24px), 500px);
		border: 1px solid rgba(0, 0, 0, 0.233);
		padding: 16px;
		border-radius: 8px;
	}

	.todo {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.deleteBtn {
		margin-inline-end: 24px;
	}
	.completeBtn {
		margin-inline-start: auto;
	}

	.completed {
		color: red;
		text-decoration: line-through;
	}

	.notComplete {
		color: black;
	}
</style>