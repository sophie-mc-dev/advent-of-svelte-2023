<script lang="ts">
	import { onMount } from 'svelte';

	import {
		Table,
		TableBody,
		TableBodyCell,
		TableBodyRow,
		TableHead,
		TableHeadCell
	} from 'flowbite-svelte';

	let children = [];
	onMount(async () => {
		children = await getTallyData();
	});

	const getTallyData = async () => {
		const response = await fetch('https://advent.sveltesociety.dev/data/2023/day-one.json');
		const tallyData = await response.json();
		return tallyData;
	};
</script>

<div>
	{#await getTallyData()}
		<p>
			<TableBodyCell>Loading...</TableBodyCell>
		</p>
	{:then data}
		<Table>
			<TableHead>
				<TableHeadCell>Child name</TableHeadCell>
				<TableHeadCell>Tally</TableHeadCell>
				<TableHeadCell>Category</TableHeadCell>
			</TableHead>
			<TableBody tableBodyClass="divide-y">
				{#each data as { name, tally }}
					<TableBodyRow>
						<TableBodyCell>{name}</TableBodyCell>
						<TableBodyCell>{tally}</TableBodyCell>
						<TableBodyCell style="color: {tally > 0 ? 'green' : 'red'}"
							>{tally > 0 ? 'Nice' : 'Naughty'}</TableBodyCell
						>
					</TableBodyRow>
				{/each}
			</TableBody>
		</Table>
	{/await}
</div>
