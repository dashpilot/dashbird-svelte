<script>
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
                <li>
                    <a href="/#/post/{item.id}" data-navigo class="block hover:bg-gray-50">
                        <div class="px-4 py-4 sm:px-6">
                            <div class="flex items-center justify-between">
                                <div class="flex-1">
                                    <p class="text-sm font-medium text-indigo-600 truncate">{item.title}</p>
                                    <div class="mt-2 flex">
                                        <div class="flex items-center text-sm text-gray-500">
                                            <svg class="flex-shrink-0 mr-1.5 h-5 w-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                                            </svg>
                                        </div>
                                    </div>
                                </div>
                                <div class="ml-5 flex-shrink-0">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">Published</span>
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-yellow-100 text-yellow-800">Draft</span>
                                </div>
                            </div>
                        </div>
                    </a>
                </li>
            {/each}
        </ul>
    </div>
</div>
