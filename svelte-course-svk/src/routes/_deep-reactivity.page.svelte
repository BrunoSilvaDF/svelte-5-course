<script lang="ts">
	let array = $state([1, 2, 3, 4, 5]);

	let objArray = $state([{ id: 1 }, { id: 2 }, { id: 3 }]);

	let obj = $state({
		name: 'John',
		age: 30,
		adress: { city: 'Brasilia', street: 'Eixo Monumental' }
	});

	$effect(() => {
		console.log('obj effect');
		console.log(obj);
	});
	$effect(() => {
		console.log('obj.name effect');
		console.log(obj.name);
	});
	$effect(() => {
		console.log('obj.adress.city');
		console.log(obj.adress.city);
	});
	$effect(() => {
		console.log('array');
		console.log(array[0]);
	});
	$effect(() => {
		console.log('array.length');
		console.log(array.length);
	});
	// $effect(() => {
	// 	// array.push(1);
	// });
</script>

<h2>{obj.name}</h2>
<h2>{obj.adress.city}</h2>

<input bind:value={obj.name} />
<input bind:value={obj.adress.city} />
<input bind:value={obj.adress.street} />
<p>{array}</p>
<button
	onclick={() => {
		array[1] = Math.random() * 10;
	}}>Add to array</button
>

<style>
	:global {
		body {
			color: white;
			font-size: 1.5em;
			background-color: #222;
		}
	}
</style>
