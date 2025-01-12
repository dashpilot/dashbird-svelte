<script>
    import PostList from '../lib/PostList.svelte';
    let { data = $bindable() } = $props();

    let selectedPage = $state('home');

    let curPosts = $derived(data.posts.filter((x) => x.page == selectedPage));

    function addPost() {
        let newItem = {};
        newItem.id = findHighestId() + 1;
        newItem.title = 'Untitled';
        newItem.page = selectedPage;
        newItem.layout = 'post';
        data.posts.push(newItem);
    }

    function findHighestId() {
        if (!data.posts || data.posts.length === 0) {
            return null; // Return null or a default value if posts are not available
        }

        return data.posts.reduce((maxId, post) => {
            return post.id > maxId ? post.id : maxId;
        }, -Infinity); // Start with a very low initial value
    }
</script>

<div class="md:flex md:items-center md:justify-between mb-6">
    <div class="flex-1 min-w-0">
        <div class="relative">
            <select bind:value={selectedPage} name="page" class="form-select">
                {#each data.pages as page (page.slug)}
                    <option value={page.slug}>
                        {page.title}
                    </option>
                {/each}
            </select>
        </div>
    </div>
    <div class="mt-4 flex md:mt-0 md:ml-4">
        <a onclick={addPost} class="ml-3 inline-flex items-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 cursor-pointer"> Create New Post </a>
    </div>
</div>

<div class="bg-white shadow rounded-lg">
    <div class="px-4 py-5 sm:px-6 border-b border-gray-200">
        <h3 class="text-lg leading-6 font-medium text-gray-900">Posts</h3>
    </div>
    <div class="bg-white shadow overflow-hidden sm:rounded-md">
        <ul class="divide-y divide-gray-200">
            {#each curPosts as item}
                <PostList {item} />
            {/each}
        </ul>
    </div>
</div>
