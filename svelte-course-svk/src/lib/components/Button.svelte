<script lang="ts">
	import type { Snippet } from 'svelte';

	let isLeftHovered = $state(false);

	interface Props {
		left?: Snippet<[boolean]>;
		right?: Snippet;
		children: Snippet<[boolean]>;
		size?: 'sm' | 'lg';
		shadow?: boolean;
	}

	let { left, right, children, size = 'sm', shadow = false, class: _class }: Props = $props();
</script>

<!-- <button class:sm={size === 'sm'} class:lg={size === 'lg'} class:shadow> -->
<!-- <button class={{ sm: size === 'sm', lg: size === 'lg', shadow }}> -->
<button class={[size === 'sm' && 'sm', size === 'lg' && 'lg', shadow && 'shadow', _class]}>
	{#if left}
		<div
			role="presentation"
			class="left"
			onmouseenter={() => (isLeftHovered = true)}
			onmouseleave={() => (isLeftHovered = false)}
		>
			{@render left(isLeftHovered)}
		</div>
	{/if}
	{@render children(isLeftHovered)}
	{#if right}
		<div class="right">
			{@render right()}
		</div>
	{/if}
</button>

<style lang="scss">
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

		&:hover {
			background-color: #0056b3;
		}
		&:disabled {
			opacity: 0.6;
			cursor: not-allowed;
		}
		&:active {
			background-image: linear-gradient(rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.1));
		}
		&.sm {
			font-size: 1rem;
			padding: 0.5rem 1rem;
			height: 45px;
		}
		&.lg {
			font-size: 1.25rem;
			padding: 0.75rem 1.5rem;
			height: 60px;
		}
		&.shadow {
			box-shadow: 0 0px 10px rgba(1, 1, 1, 0.3);
		}
		.left {
			margin-inline-end: 10px;
		}

		.right {
			margin-inline-start: 10px;
		}
	}
</style>
