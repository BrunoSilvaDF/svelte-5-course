<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';
	import { AlarmCheck, AlarmClock, Search } from 'lucide-svelte';
</script>

<!-- <DisplayName /> -->

{#snippet left()}
	<Search />
{/snippet}

<div class="wrapper">
	<Button
		size="lg"
		shadow
		--btnBgColor="yellow"
		--btnTextColor="black"
		onclick={() => alert('Clicked!')}
		onLeftHover={() => alert('Left hovered!')}
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

<style>
	:global {
		body {
			background-color: #222;
		}
	}
</style>
