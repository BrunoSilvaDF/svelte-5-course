<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import Counter from '$lib/components/Counter.svelte';
	import DisplayName from '$lib/components/DisplayName.svelte';
	import RandomNumber from '$lib/components/RandomNumber.svelte';
	import { AlarmClock, Search } from 'lucide-svelte';
</script>

<!-- <DisplayName /> -->

{#snippet left()}
	<Search />
{/snippet}

<Button>
	{#snippet left()}
		<Search />
	{/snippet}
	Meu Botão com Ícone
	{#snippet right()}
		<AlarmClock />
	{/snippet}
</Button>
