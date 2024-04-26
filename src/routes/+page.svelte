<script>
	import { Accordion, AccordionItem } from 'flowbite-svelte';
	import { Footer, FooterCopyright } from 'flowbite-svelte';
	import { Navbar, NavBrand, NavHamburger } from 'flowbite-svelte';

	import Day1 from '$lib/day1.svelte';
	import Day2 from '$lib/day2.svelte';

	const numberOfDays = 24;
	const dayComponents = [Day1, Day2];
</script>

<!-- NAVBAR -->
<Navbar class="fixed start-0 top-0 z-20 mb-4 w-full border-b px-2 py-2.5 sm:px-4">
	<NavBrand href="https://advent.sveltesociety.dev/#challenges">
		<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white"
			>Advent of Svelte</span
		>
	</NavBrand>
	<NavHamburger />
	<span>by <b>sophie-mc-dev</b></span>
</Navbar>

<!-- MAIN CONTENT -->
<main class="mb-10 mt-20 flex flex-col items-center p-4">
	<div class="w-full md:w-3/4 lg:w-1/2">
		<Accordion>
			{#each Array.from({ length: numberOfDays }, (_, index) => index + 1) as day}
				<AccordionItem>
					<span slot="header">Day {day}</span>
					<svelte:component this={dayComponents[day - 1]} />
				</AccordionItem>
			{/each}
		</Accordion>
	</div>
</main>

<!-- FOOTER -->
<Footer>
	<FooterCopyright href="https://github.com/sophie-mc-dev" by="sophie-mc-dev" year={2024} />
</Footer>
