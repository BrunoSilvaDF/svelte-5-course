<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';
	import { AlarmCheck, AlarmClock, Search } from 'lucide-svelte';

	let btn: Button;

	$effect(() => {
		console.log('Button component instance:', btn.getButton());
	});
</script>

<!-- <DisplayName /> -->

{#snippet left()}
	<Search />
{/snippet}

<div class="wrapper">
	<div
		role="presentation"
		onclick={(e) => {
			e.stopPropagation();
			console.log('evt comming from div');
		}}
	>
		<Button
			bind:this={btn}
			href="https://svelte.dev"
			size="lg"
			shadow
			--btnBgColor="yellow"
			--btnTextColor="black"
			onclick={(e) => {
				e.stopPropagation();
				console.log('evt comming from button');
			}}
		>
			{#snippet left(isHovered: boolean)}
				{#if isHovered}
					<Search />
				{:else}
					<AlarmCheck />
				{/if}
			{/snippet}
			Text
			{#snippet right()}
				<AlarmClock />
			{/snippet}
		</Button>
	</div>
</div>

<style>
	:global {
		body {
			background-color: #222;
		}
	}
</style>
