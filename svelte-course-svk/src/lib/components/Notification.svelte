<script lang="ts">
	import Button from './Button.svelte';

	let {
		notification,
		onremove
	}: {
		notification: {
			id: string;
			title: string;
			body: string;
			date: number;
		};
		onremove?: (id: string) => void;
	} = $props();
</script>

<div class="notification">
	<input type="text" bind:value={notification.title} />
	<h5>{notification.title}</h5>
	<p>{notification.body}</p>
	<time datetime={new Date(notification.date).toISOString()}>
		{new Date(notification.date).toLocaleDateString()}
	</time>
	<div class="actions">
		<Button --btnBgColor="rgb(218, 84, 84)" onclick={() => onremove?.(notification.id)}>
			Remove
		</Button>
	</div>
</div>

<style>
	.notification {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}
	.actions {
		display: flex;
		justify-content: flex-end;
		gap: 10px;
	}
</style>
