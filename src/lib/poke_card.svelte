<script>
	export let pokemon;

	async function fetchData() {
		const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemon}`);
		let data = await response.json();
		data.name = data.name.charAt(0).toUpperCase() + data.name.slice(1);
		return data;
	}
</script>

{#await fetchData() then data}
	<div
		class="max-w-md bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-100 dark:border-gray-300 m-3"
	>
		<p class="m-4">{data.id}</p>
		<div class="flex flex-col items-center pb-8">
			<img class="mb-2 w-24 h-24" src={data.sprites.front_default} alt={data.name} />
			<h5 class="mb-1 text-2xl font-large text-gray-900 dark:text-black">{data.name}</h5>
			<span class="text-sm text-gray-400 dark:text-gray-600">
				{#each data.types as type}
					<span class="text-md">{type.type.name} &nbsp; &nbsp;</span>
				{/each}
			</span>
			<div class="flex mt-4 space-x-3 md:mt-6">
				<a
					href="#"
					class="inline-flex items-center py-2 px-4 text-sm font-medium text-center text-blue-900 bg-blue-200 rounded-lg hover:bg-blue-300 focus:ring-4 focus:outline-none focus:ring-blue-200 dark:bg-blue-300 dark:hover:bg-blue-500 dark:focus:ring-blue-800"
					>Add</a
				>
				<a
					href="#"
					class="inline-flex items-center py-2 px-4 text-sm font-medium text-center text-gray-900 bg-white rounded-lg border border-gray-300 hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-gray-200 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-700 dark:focus:ring-gray-700"
					>Details</a
				>
			</div>
		</div>
	</div>
{/await}
