<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLAnchorAttributes, HTMLButtonAttributes } from 'svelte/elements';

	let isLeftHovered = $state(false);

	type Props = (
		| (HTMLButtonAttributes & { href?: never })
		| (HTMLAnchorAttributes & { href: string })
	) & {
		left?: Snippet<[boolean]>;
		right?: Snippet;
		children: Snippet<[boolean]>;
		size?: 'sm' | 'lg';
		shadow?: boolean;
		bgColor?: string;
		textColor?: string;
		onLeftHover?: () => void;
	};

	let btn: HTMLButtonElement | HTMLAnchorElement;

	let {
		left,
		right,
		children,
		size = 'sm',
		shadow = false,
		class: _class,
		onLeftHover,
		...props
	}: Props = $props();

	export function focus() {
		btn.focus();
	}

	export function getButton() {
		return btn;
	}
</script>

<!-- <button class:sm={size === 'sm'} class:lg={size === 'lg'} class:shadow> -->
<!-- <button class={{ sm: size === 'sm', lg: size === 'lg', shadow }}> -->
<svelte:element
	this={props.href ? 'a' : 'button'}
	bind:this={btn}
	class={['button', size === 'sm' && 'sm', size === 'lg' && 'lg', shadow && 'shadow', _class]}
	{...props}
>
	<div class="flex">
		{#if left}
			<div
				role="presentation"
				class="left"
				onmouseenter={() => {
					onLeftHover?.();
					isLeftHovered = true;
				}}
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
	</div>
</svelte:element>

<style lang="scss">
	.button {
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 0.5rem 1rem;
		background-color: var(--btnBgColor, #007bff);
		color: var(--btnTextColor, #fff);
		border: none;
		border-radius: 4px;
		cursor: pointer;
		display: inline-block;
		font-size: 1rem;
		font-family: sans-serif;
		text-decoration: none;

		.flex {
			display: flex;
			align-items: center;
			justify-content: center;
			height: 100%;
		}

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
