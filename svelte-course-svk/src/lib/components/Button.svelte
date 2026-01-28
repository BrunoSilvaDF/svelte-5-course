<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		left?: Snippet;
		right?: Snippet;
		children: Snippet;
	}
	let { left, right, children }: Props = $props();
</script>

<button>
	{#if left}
		<div class="left">
			{@render left()}
		</div>
	{/if}
	{@render children()}
	{#if right}
		<div class="right">
			{@render right()}
		</div>
	{/if}
</button>

<style>
	button {
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 0.5rem 1rem;
		background-color: #007bff;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		font-size: 1rem;
	}

	button:hover {
		background-color: #0056b3;
	}

	.left {
		margin-inline-end: 10px;
	}

	.right {
		margin-inline-start: 10px;
	}
</style>
