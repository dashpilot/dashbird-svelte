<script>
    let { mydata } = $props();

    async function save() {
        if (mydata) {
            try {
                const response = await fetch('/api/save', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(mydata),
                });

                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }

                const data = await response.json();
                console.log('Success:', data);
            } catch (error) {
                console.error('Error:', error);
            }
        }
    }
</script>

<button type="button" class="bg-indigo-600 border border-transparent rounded-md shadow-sm py-2 px-4 inline-flex justify-center text-sm font-medium text-white hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500" onclick={save}>Save</button>
