<script>

    export let name = 'empty';
    export let priority = 'empty';
    export let state;
    
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    
</script>


<div class='card container rounded-md border-2 border-gray-300 bg-[#101210] p-4 text-[#15616D] flex justify-between'>
    <!-- if priority is high, make the text red -->
    <p class={priority === 'high' ? 'text-red-500' : ''}>{name}, {priority}</p>
    <div>
        
        <button class='rounded-md bg-[#15616D] p-2 text-white transition-colors duration-200 hover:bg-green-500 active:bg-[#104952]' on:click={() => dispatch('markDone', name)}>{state}</button>
        <button class='rounded-md bg-[#15616D] p-2 text-white transition-colors duration-200 hover:bg-red-500 active:bg-[#104952]' on:click={() => dispatch('removeTodo', name)}>Delete</button>
        
    </div>

</div>