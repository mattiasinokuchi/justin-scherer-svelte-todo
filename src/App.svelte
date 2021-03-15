<!-- This file contain logic for the whole application -->

<script>
    import Todo from './Todo.svelte';

    let newTodoText = '';
    let newTodoDate = null;
    let currSize = 0;
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
</script>

<style></style>

<h1>Todo Application! <span> Current number of Todos: {currSize}</span></h1>
<ul id="main"></ul>
<button on:click={addTodo}>Add Todo</button>
<input type="text" bind:value={newTodoText}/>
<input type="date" bind:value={newTodoDate} />