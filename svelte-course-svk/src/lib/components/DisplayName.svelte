<script lang="ts">
	let firstName = $state('Bruno');
	let lastName = $state('Silva');
	let name = $derived.by(() => {
		console.log('full name derived');
		return `${firstName} ${lastName}`;
	});
	let username = $state('brunosilva');
	let src = 'https://picsum.photos/200';
	let bio = '<p>This is <strong>my</strong> bio</p>';

	$effect(() => {
		if (username || name) {
			console.log('Username or full name changed');
		}
	});
</script>

<!-- <img {src} alt="Random Stuff" /> -->
<input bind:value={username} />
<input
	value={firstName}
	oninput={(e) => {
		firstName = e.currentTarget.value;
		name = 'blah';
		console.log(name);
	}}
/>
<input bind:value={lastName} />

<h1>{username || name}</h1>

<p>{@html bio}</p>

<button onclick={() => console.log(name)}>Get fullname</button>

<style>
	h1 {
		color: purple;
	}
</style>
