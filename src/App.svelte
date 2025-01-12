<script>
    import { onMount } from 'svelte';
    import Navigo from 'navigo'; // When using ES modules.

    import Dashboard from './pages/Dashboard.svelte';
    import Posts from './pages/Posts.svelte';
    import Post from './pages/Post.svelte';
    import Pages from './pages/Pages.svelte';
    import Settings from './pages/Settings.svelte';

    let route = $state('home');
    let data = $state();
    let id = $state();

    onMount(async () => {
        try {
            const response = await fetch('/data.json');
            if (!response.ok) {
                throw new Error('Network response was not ok');
            }
            data = await response.json();
        } catch (error) {
            console.error('There was a problem with the fetch operation:', error);
        }

        const router = new Navigo('/', { hash: true });

        router.on('/', function () {
            route = 'dashboard';
        });

        router.on('/posts', function () {
            route = 'posts';
        });

        router.on('/post/:id', function (data) {
            id = data.data.id;
            route = 'post';
        });

        router.on('/pages', function () {
            route = 'pages';
        });

        router.on('/settings', function () {
            route = 'settings';
        });

        router.resolve();
    });
</script>

<div class="min-h-screen flex bg-gray-50">
    <!-- Sidebar -->
    <aside class="bg-gray-800 w-64 flex flex-col fixed h-full">
        <div class="p-4">
            <h1 class="text-white text-2xl font-bold pl-2">DashBird CMS</h1>
        </div>
        <nav class="flex-1 px-2 py-4">
            <a href="/" data-navigo class="flex items-center px-4 py-2 text-gray-100 hover:bg-gray-700 rounded-lg mb-1" active-class="bg-gray-700">
                <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
                </svg>
                Dashboard
            </a>
            <a href="/posts" data-navigo class="flex items-center px-4 py-2 text-gray-100 hover:bg-gray-700 rounded-lg mb-1">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5 mr-3">
                    <path d="M13.4 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-7.4" />
                    <path d="M2 6h4" />
                    <path d="M2 10h4" />
                    <path d="M2 14h4" />
                    <path d="M2 18h4" />
                    <path d="M21.378 5.626a1 1 0 1 0-3.004-3.004l-5.01 5.012a2 2 0 0 0-.506.854l-.837 2.87a.5.5 0 0 0 .62.62l2.87-.837a2 2 0 0 0 .854-.506z" />
                </svg>
                Posts
            </a>

            <a href="/pages" data-navigo class="flex items-center px-4 py-2 text-gray-100 hover:bg-gray-700 rounded-lg mb-1" active-class="bg-gray-700">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5 mr-3">
                    <path d="M15 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7Z" />
                    <path d="M14 2v4a2 2 0 0 0 2 2h4" />
                </svg>
                Pages
            </a>

            <!--
          <a href="#" class="flex items-center px-4 py-2 text-gray-100 hover:bg-gray-700 rounded-lg mb-1">
              <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
              </svg>
              Users
          </a>
          -->
            <a href="/settings" data-navigo class="flex items-center px-4 py-2 text-gray-100 hover:bg-gray-700 rounded-lg" active-class="bg-gray-700">
                <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"
                    ></path>
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                </svg>
                Settings
            </a>
        </nav>
    </aside>

    <!-- Main Content -->
    <div class="flex-1 ml-64">
        <!-- Header -->
        <header class="bg-white shadow-sm">
            <div class="max-w-7xl mx-auto py-4 px-4 sm:px-6 lg:px-8 flex justify-between items-center">
                <h2 class="text-xl font-semibold text-gray-800">Dashboard</h2>
                <div class="flex items-center">
                    <button class="flex items-center text-gray-500 hover:text-gray-700">
                        <span class="mr-2">John Doe</span>
                        <div class="h-8 w-8 rounded-full bg-indigo-500"></div>
                    </button>
                </div>
            </div>
        </header>

        <!-- Main Content Area -->
        <main class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
            {#if route == 'dashboard'}
                <Dashboard bind:data />
            {:else if route == 'posts'}
                <Posts bind:data />
            {:else if route == 'post'}
                <Post bind:data {id} />
            {:else if route == 'pages'}
                <Pages bind:data />
            {:else if route == 'settings'}
                <Settings bind:data />
            {/if}
        </main>
    </div>
</div>
