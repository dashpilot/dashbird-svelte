<script>
    let { data = $bindable() } = $props();

    import SaveBtn from '../lib/SaveBtn.svelte';

    function addPage() {
        data.pages = [...data.pages, { title: '', slug: '' }];
    }

    function deletePage(index) {
        data.pages = data.pages.filter((_, i) => i !== index);
    }

    function slugify(event, index) {
        const title = event.target.value;
        data.pages[index].slug = title.toLowerCase().replace(/\s+/g, '-');
    }

    const baseClasses = 'w-full rounded-lg border border-gray-300 shadow-sm focus:border-blue-500 focus:ring-1 focus:ring-blue-500 bg-white px-4 py-2 mt-0 mb-5 resize-none text-gray-900';
</script>

<div class="flex items-center justify-between mb-6">
    <div class="flex-1 min-w-0">
        <h2 class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate">Pages</h2>
    </div>
    <div>
        <SaveBtn mydata={data} />
    </div>
</div>

<!-- Editor Form -->
<div class="bg-white shadow sm:rounded-lg">
    <div class="px-4 py-5 sm:p-6">
        <form>
            <div>
                <button type="button" onclick={addPage} class="border border-gray-300 text-gray-500 hover:bg-gray-500 hover:text-white font-medium py-2 px-2 rounded mb-4">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-plus">
                        <path d="M5 12h14" />
                        <path d="M12 5v14" />
                    </svg>
                </button>

                {#each data.pages as page, index (index)}
                    <div class="flex">
                        <div class="w-1/2 pr-3">
                            <input type="text" name="title" bind:value={page.title} class={baseClasses} oninput={(e) => slugify(e, index)} />
                        </div>
                        <div class="w-1/2 pr-3">
                            <input type="text" name="title" value={page.slug} class={`${baseClasses} bg-gray-100 text-gray-400 border-gray-300 cursor-not-allowed`} disabled />
                        </div>
                        <div>
                            <button type="button" onclick={() => deletePage(index)} class="border border-gray-300 text-gray-500 hover:bg-gray-500 hover:text-white font-medium py-2 px-2 rounded">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-minus">
                                    <path d="M5 12h14" />
                                </svg>
                            </button>
                        </div>
                    </div>
                {/each}
            </div>
        </form>
    </div>
</div>
