<script>
    import Todo from './Todo.svelte';

    let newTodoText = '';
    const Todos = new Set();

    function addTodo() {
        const todo = new Todo({
            target: document.querySelector('#main'),
            props: {
                num: Todo.size,
                description: newTodoText
            }
        });
        newTodoText = '';
        todo.$on('remove', () => {
            Todos.delete(todo);
            todo.$destroy();
        });
        Todos.add(todo);
    }
</script>

<style></style>

<h1>Todo Application!</h1>
<ul id="main"></ul>
<button on:click={addTodo}>Add Todo</button>
<input type="text" bind:value={newTodoText}/>