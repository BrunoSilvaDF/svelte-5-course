<script lang="ts">
	let count = $state(0);
	let frequency = $state(1000);
	let paused = $state(false);

	$effect(() => {
		if (paused) return;
		const interval = setInterval(() => {
			count += 1;
		}, frequency);
		return () => clearInterval(interval);
	});
</script>

<h1>{count}</h1>
<h2>{frequency}</h2>

<button
	onclick={() => {
		count = 0;
		const originalFrequency = frequency;
		frequency = 1001;
		frequency = originalFrequency;
	}}>Reset</button
>
<button onclick={() => (paused = !paused)}>{paused ? 'Resume' : 'Pause'}</button>

<button onclick={() => (frequency *= 2)}>Slower</button>
<button onclick={() => (frequency /= 2)}>Faster</button>
