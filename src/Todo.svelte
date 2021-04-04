<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    export let item = {};

    const onDelete = ev => dispatch('todoDelete', ev.target.attributes['data-id'].value);
    const onCompletedChanged = ev => dispatch('todoCompletedChanged', ev.target.attributes['data-id'].value);
</script>
<main>
    <li>
        <input type="checkbox" bind:checked={item.completed} on:change={onCompletedChanged} data-id={item.id}>
        <span class={item.completed ? 'completed' : ''}>{item.description}</span>
        <button on:click={onDelete} data-id={item.id}>Delete</button>
    </li>
</main>
<style>
    .completed {
        text-decoration: line-through;
    }
</style>
