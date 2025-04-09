<script>
	import Todo from './Todo.svelte';

	let todo = [];

    let done_todo = [];

	let newTodo = '';
    let selectedPriority = 'low';
    
	function addTodo() {
		todo.push({
			name: newTodo,
			priority: selectedPriority
		});
		todo = todo;
		newTodo = '';
	}

	function removeTodo(todo_name) {
        todo = todo.filter((t) => t.name !== todo_name);
        done_todo = done_todo.filter((t) => t.name !== todo_name);
        todo = todo;
        done_todo = done_todo;
	}

    function markDone(todo_name) {
        if (done_todo.find((t) => t.name === todo_name)) {
            todo.push({
                name: todo_name,
                priority: done_todo.find((t) => t.name === todo_name).priority
            });
            todo = todo;    
            done_todo = done_todo.filter((t) => t.name !== todo_name);
            done_todo = done_todo;
        }
        else {
            done_todo.push({
                name: todo_name,
                priority: todo.find((t) => t.name === todo_name).priority
            });
            todo = todo.filter((t) => t.name !== todo_name);
            todo = todo;
            done_todo = done_todo;
        }
    }


	function clearTodo() {
		todo = [];
        done_todo = [];
	}
</script>

<div class="flex h-screen justify-center bg-[#FFDDAD]">
	<div class="card container rounded-md border-2 border-gray-300 bg-[#001524] p-4 text-[#15616D]">
		<h1 class="text-2xl font-bold">Todo List</h1>

		<div class="flex justify-center">
			<input
				class="rounded-md border-2 border-gray-300 bg-[#001524] p-2 text-[#15616D]"
				type="text"
				bind:value={newTodo}
			/>

            <!-- add priority selector -->
            <select class="rounded-md border-2 border-gray-300 bg-[#001524] p-2 text-[#15616D]" bind:value={selectedPriority}>
                <option value="low">Low</option>
                <option value="medium">Medium</option>
                <option value="high">High</option>
            </select>
            
			<button
				class="rounded-md bg-[#15616D] p-2 text-white transition-colors duration-200 hover:bg-[#1a7a89] active:bg-[#104952]"
				on:click={addTodo}>Add Todo</button
			>
			<button
				class="rounded-md bg-[#15616D] p-2 text-white transition-colors duration-200 hover:bg-[#1a7a89] active:bg-[#104952]"
				on:click={clearTodo}>Clear Todo</button
			>
		</div>
		<ul>
			{#each todo as todo}
				<div class="h-4"></div>
				<Todo state={"Done"} name={todo.name} priority={todo.priority} on:removeTodo={(e) => removeTodo(e.detail)} on:markDone={(e) => markDone(e.detail)} />
			{/each}
		</ul>

        <div class="h-4"></div>

        <h1 class="text-2xl font-bold">Done</h1>
        <ul>
            {#each done_todo as todo}
                <div class="h-4"></div>
                <Todo state={"Undone"} name={todo.name} priority={todo.priority} on:removeTodo={(e) => removeTodo(e.detail)} on:markDone={(e) => markDone(e.detail)}/>
            {/each}
        </ul>
	</div>
</div>
