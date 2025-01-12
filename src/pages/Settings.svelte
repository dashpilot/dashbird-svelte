<script>
    import SaveBtn from '../lib/SaveBtn.svelte';
    let { data = $bindable() } = $props();

    const baseClasses = 'w-full rounded-lg border border-gray-300 shadow-sm focus:border-blue-500 focus:ring-1 focus:ring-blue-500 bg-white px-4 py-2 mt-0 mb-5 resize-none text-gray-900';
</script>

<div class="flex items-center justify-between mb-6">
    <div class="flex-1 min-w-0">
        <h2 class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate">Settings</h2>
    </div>
    <div>
        <SaveBtn mydata={data} />
    </div>
</div>

<div class="bg-white shadow sm:rounded-lg">
    <div class="px-4 py-5 sm:p-6">
        {#each data.settings as item}
            <label for="status" class="block text-sm font-medium text-gray-700 mb-1 capitalize">{item.key.replaceAll('_', ' ')}</label>
            <input type="text" class={baseClasses} bind:value={item.value} />
        {/each}
    </div>
</div>
