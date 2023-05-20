<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher()
    
    let id = 0
    let task
    let completed = false

    function generateRandomNumber(x) {
        return x = Math.floor(Math.random() * 100) + 1
    }

    function addNewTodo() {
        const todo = {
            id: generateRandomNumber(id),
            task,
            completed,
        }

        dispatch('addingNewTodo', todo)
        task = ''
    }
</script>

<h1>TODO</h1>

<form on:submit|preventDefault={addNewTodo}>
    <input type="text" bind:value={task} placeholder="create new todo">
    <button type="submit">Add</button>
</form>

<style lang="scss">
    h1 {
        color: red;
    }
</style>