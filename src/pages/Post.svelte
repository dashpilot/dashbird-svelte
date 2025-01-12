<script>
    import SaveBtn from '../lib/SaveBtn.svelte';
    let { data = $bindable(), id } = $props();

    let item = $derived(data.posts.filter((x) => x.id == id)[0]);

    const baseClasses = 'w-full rounded-lg border border-gray-300 shadow-sm focus:border-blue-500 focus:ring-1 focus:ring-blue-500 bg-white px-4 py-2 mt-0 mb-5 resize-none text-gray-900';
</script>

{#if item}
    <div class="flex items-center justify-between mb-6">
        <div class="flex-1 min-w-0">
            <h2 class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate">Settings</h2>
        </div>
        <div><SaveBtn mydata={data} /></div>
    </div>

    <!-- Editor Form -->
    <div class="bg-white shadow sm:rounded-lg">
        <div class="px-4 py-5 sm:p-6">
            <form spellcheck="false">
                <div class="space-y-6">
                    <div>
                        <label for="title" class="block text-sm font-medium text-gray-700 mb-1">Title</label>
                        <input type="text" name="title" id="title" class={baseClasses} placeholder="Post title" bind:value={item.title} />
                    </div>

                    <div>
                        <label for="excerpt" class="block text-sm font-medium text-gray-700 mb-1">Excerpt</label>
                        <div class="mt-1">
                            <textarea id="excerpt" name="excerpt" rows="3" class={baseClasses} placeholder="Brief excerpt for your post..."></textarea>
                        </div>
                    </div>

                    <div>
                        <label for="content" class="block text-sm font-medium text-gray-700 mb-1">Body</label>
                        <div class="mt-1">
                            <textarea id="content" name="content" rows="15" class={baseClasses} placeholder="Write your post content here..." bind:value={item.body}></textarea>
                        </div>
                    </div>

                    <div>
                        <label for="status" class="block text-sm font-medium text-gray-700 mb-1">Status</label>
                        <select id="status" name="status" class={baseClasses} bind:value={item.draft}>
                            <option value="true">Draft</option>
                            <option value="false">Published</option>
                        </select>
                    </div>
                </div>
            </form>
        </div>
    </div>
{/if}
