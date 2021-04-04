<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    export let item = {};
    const onDelete = (ev) => {
        dispatch('todo-delete', ev.target.attributes['data-id'].value);
    };
    const onCompletedChanged = (ev) => {
        dispatch('todo-completed-changed', ev.target.attributes['data-id'].value);
    }
</script>
<main>
    <li>
        <input type="checkbox" bind:checked={item.completed} on:change={onCompletedChanged} data-id={item.id}>
        <span style="text-decoration: {item.completed ? 'line-through' : ''}">{item.description}</span>
        <button on:click={onDelete} data-id={item.id}>Delete</button>
    </li>
</main>
<style></style>
