<script lang="ts">
	import { tick, untrack } from 'svelte';

	let randomNumber = $state(Math.floor(Math.random() * 10));
	let doubleRandomNumber = $derived(2 * randomNumber);
	// let doubleRandomNumber = $state();

	let history: number[] = $state([untrack(() => randomNumber)]);
	let historyPTag: HTMLParagraphElement;

	// $effect(() => {
	// 	doubleRandomNumber = randomNumber * 2;
	// });

	// $effect(() => {
	// 	randomNumber;
	// 	untrack(() => {
	// 		history.push(randomNumber);
	// 	});
	// });

	$effect.pre(() => {
		history.length;
		console.log('$effect.pre', historyPTag?.innerText);
		tick().then(() => {
			console.log('$effect.pre tick', historyPTag?.innerText);
		});
		return () => {
			console.log('$effect.pre cleanup', historyPTag?.innerText);
		};
	});

	$effect(() => {
		history.length;
		console.log('$effect', historyPTag?.innerText);
		return () => {
			console.log('$effect cleanup', historyPTag?.innerText);
		};
	});
</script>

<h2>Random Number: {randomNumber}</h2>
<h2>Double Random Number: {doubleRandomNumber}</h2>

<p bind:this={historyPTag}>{history.join(', ')}</p>

<button
	onclick={() => {
		randomNumber = Math.floor(Math.random() * 10);
		history = [...history, randomNumber];
		// console.log('randomNumber, doubleRandomNumber :>> ', randomNumber, doubleRandomNumber);
	}}>Generate</button
>
