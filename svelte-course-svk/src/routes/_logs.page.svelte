<script lang="ts">
	let array = $state([1, 2, 3, 4, 5]);

	let objArray = $state([{ id: 1 }, { id: 2 }, { id: 3 }]);

	let obj = $state({
		name: 'John',
		age: 30,
		adress: { city: 'Brasilia', street: 'Eixo Monumental' }
	});

	// $inspect(obj).with(console.trace);

	// $effect(() => {
	// 	$inspect.trace();
	// 	console.log(obj.name);
	// 	console.log(obj.adress.city);
	// });
</script>

{@debug obj, array}
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

<button
	onclick={() => {
		console.log($state.snapshot(obj));
	}}
>
	Log Snapshot
</button>

<style>
	:global {
		body {
			color: white;
			font-size: 1.5em;
			background-color: #222;
		}
	}
</style>
