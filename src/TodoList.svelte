<script>
	import Todo from './Todo.svelte';

	let todos = [
		{id:1, description: 'learn svelte', completed:true, active:true},
		{id:2, description:'build a todo app', completed: false, active:true},
		{id:3, description:'learn tailwind', completed: false, active: true}
	];
	let newTaskDescription = '';
	let activeTodos = [];
	let incompletedCount = 0;
	let completedCount = 0;

	const addTask = () => {
		if(!newTaskDescription.trim().length) return;
		const id = todos.map((i) => i.id).reduce( (p,v)=> p>v ? p : v ) + 1;
		todos.push({id: id, description:newTaskDescription, completed:false, active: true});
		updateActiveList();
		newTaskDescription = '';
	}
	const deleteTask = (ev) => {
		todos.forEach(i => { if(i.id == ev.detail) i.active = false });
		updateActiveList();
	}

	const archiveCompleted = () => {
		todos.forEach(i => { if(i.completed) i.active = false });
		updateActiveList()
	}

	const completedChanged = () => {
		updateCounts();
	}
    const updateActiveList = () => {
		activeTodos = todos.filter((i) => i.active);
		updateCounts();
	}
	const updateCounts = () => {
		incompletedCount = activeTodos.filter(i => !i.completed).length;
		completedCount = activeTodos.filter(i => i.completed).length;
	}

    updateActiveList();
    updateCounts();
</script>

<main>
	<div>
		<span>{incompletedCount} of {activeTodos.length} remaining</span>
		<button on:click={archiveCompleted} disabled={completedCount==0}>Archive Completed</button>
	</div>
	<div>
		<input type="text" bind:value={newTaskDescription} placeholder="enter new todo here" >
		<button on:click={addTask} disabled={newTaskDescription.trim().length==0}>Add</button>
	</div>

	<ul>
		{#each activeTodos as item, index (item.id)}
		<Todo item={item} on:todo-delete={deleteTask} on:todo-completed-changed={completedChanged}></Todo>
		{/each}
	</ul>

</main>

<style>
	ul {
		list-style: none;
	}

</style>
