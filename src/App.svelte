<!-- This file contain logic for the whole application -->

<script>
    import Todo from './Todo.svelte';

    let newTodoText = '';
    let newTodoDate = null;
    let currSize = 0;
    let completed = false;
    let overdue = false;
    const Todos = new Set();

    function addTodo() {
        const todo = new Todo({
            target: document.querySelector('#main'),
            props: {
                num: currSize + 1,
                dueDate: newTodoDate,
                description: newTodoText
            }
        });
        handleHide(todo);
        newTodoText = '';
        newTodoDate = null;
        todo.$on('remove', () => {
            Todos.delete(todo); // reset text
            currSize = Todos.size;
            todo.$destroy(); //prevent memory leak
        });
        Todos.add(todo);
        currSize = Todos.size;
    }

    function handleHide(item) {
        const currDate = Date.now();
        if (completed && overdue) {
            item.hidden = !item.completed || new Date(item.dueDate).getTime() < currDate;
            return;
        }
        if (completed) {
            item.hidden = !item.completed;
            return;
        }
        if (overdue) {
            item.hidden = new Date(item.dueDate).getTime() < currDate;
            return;
        }
        item.hidden = false;
    }

    function handleFilter() {
        for (const item of Todos) {
            handleHide(item);
        }
    }
</script>

<style></style>

<h1>Todo Application! <span> Current number of Todos: {currSize}</span></h1>
<ul id="main"></ul>
<button on:click={addTodo}>Add Todo</button>
<input type="text" bind:value={newTodoText}/>
<input type="date" bind:value={newTodoDate} />
<label>
    <input type="checkbox" bind:checked={completed} on:change={handleFilter}/>
    Completed
</label>
<label>
    <input type="checkbox" bind:checked={overdue} on:change={handleFilter}>
    Overdue
</label>