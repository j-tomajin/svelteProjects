<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher()
    
    let id = 0
    let task = ''
    let completed = false

    let selected
    let options = [
        {
            id: 1,
            option: 'All',
            selected: true,
        },
        {
            id: 2,
            option: 'active',
            selected: false,
        },
        {
            id: 3,
            option: 'completed',
            selected: false,
        }
    ]

    function generateRandomNumber(x) {
        return x = Math.floor(Math.random() * 100) + 1
    }

    function addNewTodo() {
        if(task == '') return
        const todo = {
            id: generateRandomNumber(id),
            task,
            completed,
        }

        dispatch('addingNewTodo', todo)
        dispatch('optionsDispatch', options)
        task = ''
    }
</script>

<h1>TODO</h1>

<form on:submit|preventDefault={addNewTodo}>
    <input type="text" bind:value={task} placeholder="create new todo">
    
    <select bind:value={selected}>
        {#each options as option (option.id)}
            <option value={option}>{option.option}</option>
        {/each}
    </select>
    <button type="submit">Add</button>
</form>

<style lang="scss">
    input {
        width: 50%;
    }

    h1 {
        text-align: center;
        color: rgb(0, 209, 209);
    }
</style>