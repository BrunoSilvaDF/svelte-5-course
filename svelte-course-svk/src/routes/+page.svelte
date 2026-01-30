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

<Button size="lg" shadow={true} class={{ 'my-custom-class': true }}>
	{#snippet left(isHovered: boolean)}
		{#if isHovered}
			<Search />
		{:else}
			<AlarmCheck />
		{/if}
	{/snippet}
	{#snippet children(isHovered: boolean)}
		Text {isHovered}
	{/snippet}
	{#snippet right()}
		<AlarmClock />
	{/snippet}
</Button>
