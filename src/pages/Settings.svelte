<script>
    import Nav from '../lib/Nav.svelte';
    let { data = $bindable() } = $props();

    const baseClasses = 'w-full rounded-lg border border-gray-300 shadow-sm focus:border-blue-500 focus:ring-1 focus:ring-blue-500 bg-white px-4 py-2 mt-0 mb-5 resize-none text-gray-900';
</script>

{#each data.settings as item}
    <label for="status" class="block text-sm font-medium text-gray-700 mb-1 capitalize">{item.key.replaceAll('_', ' ')}</label>
    <input type="text" class={baseClasses} bind:value={item.value} />
{/each}
