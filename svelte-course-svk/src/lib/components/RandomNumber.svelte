<script lang="ts">
	import { untrack } from 'svelte';

	let randomNumber = $state(Math.floor(Math.random() * 10));
	let doubleRandomNumber = $derived(2 * randomNumber);
	// let doubleRandomNumber = $state();

	let history: number[] = $state([untrack(() => randomNumber)]);

	// $effect(() => {
	// 	doubleRandomNumber = randomNumber * 2;
	// });

	// $effect(() => {
	// 	randomNumber;
	// 	untrack(() => {
	// 		history.push(randomNumber);
	// 	});
	// });
</script>

<h2>Random Number: {randomNumber}</h2>
<h2>Double Random Number: {doubleRandomNumber}</h2>

<p>{history.join(', ')}</p>

<button
	onclick={() => {
		randomNumber = Math.floor(Math.random() * 10);
		history = [...history, randomNumber];
		console.log('randomNumber, doubleRandomNumber :>> ', randomNumber, doubleRandomNumber);
	}}>Generate</button
>
