<script lang="ts">
	import Notification from '$lib/components/Notification.svelte';
	import generateNotifications from '$lib/utils/generate-notifications';

	let notifications = $state(generateNotifications(3));
</script>

<ul>
	{#each notifications as notification, idx (notification.id)}
		<li class="notification">
			<Notification
				{notification}
				onremove={() => {
					notifications.splice(idx, 1);
				}}
			/>
		</li>
	{:else}
		<li class="empty">No notifications</li>
	{/each}
</ul>

<style>
	ul {
		list-style: none;
		padding: 10px;
		margin: 0;
		li {
			margin-bottom: 10px;
			padding: 10px;
			background-color: #333;
			border-radius: 5px;
		}
	}
	:global {
		body {
			color: white;
			font-size: 1.5em;
			background-color: #222;
		}
	}
</style>
