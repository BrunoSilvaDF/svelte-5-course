<script lang="ts">
	import dummyRates from '$lib/utils/dummy-rates';

	let baseValue: number | undefined = $state(1);
	let baseCurrency = $state('usd');
	let baseRates = $derived(dummyRates[baseCurrency]);
	let targetCurrency = $state('eur');
	let targetValue: number | undefined = $state(calculateTarget());

	function calculateTarget() {
		return baseValue && baseRates[targetCurrency] && baseValue * baseRates[targetCurrency];
	}

	function calculateBase() {
		return targetValue && baseRates[targetCurrency] && targetValue / baseRates[targetCurrency];
	}

	// $effect(() => {
	// 	targetValue = baseValue && baseRates[targetCurrency] && baseValue * baseRates[targetCurrency];
	// 	console.log(
	// 		'Calculating Target',
	// 		untrack(() => targetValue)
	// 	);
	// });
	// $effect(() => {
	// 	baseValue = targetValue && baseRates[targetCurrency] && targetValue / baseRates[targetCurrency];
	// 	console.log(
	// 		'Calculating Base',
	// 		untrack(() => baseValue)
	// 	);
	// });
</script>

<div class="wrapper">
	<div class="conversion">
		<span class="base"
			>{Number(1).toLocaleString('en-US', {
				style: 'currency',
				currency: baseCurrency,
				currencyDisplay: 'name'
			})} equals</span
		>
		<span class="target"
			>{baseRates[targetCurrency].toLocaleString('en-US', {
				style: 'currency',
				currency: targetCurrency,
				currencyDisplay: 'name'
			})}</span
		>
	</div>
	<div class="base">
		<input
			type="number"
			value={baseValue}
			oninput={(e) => {
				baseValue = (e.target as HTMLInputElement).valueAsNumber;
				targetValue = calculateTarget();
			}}
		/>
		<select
			bind:value={baseCurrency}
			oninput={(e) => {
				baseCurrency = (e.target as HTMLSelectElement).value;
				targetValue = calculateBase();
			}}
		>
			<option value="usd">USD</option>
			<option value="eur">EUR</option>
			<option value="gbp">GBP</option>
		</select>
	</div>
	<div class="target">
		<input
			type="number"
			value={targetValue}
			oninput={(e) => {
				targetValue = (e.target as HTMLInputElement).valueAsNumber;
				baseValue = calculateBase();
			}}
		/>
		<select
			bind:value={targetCurrency}
			oninput={(e) => {
				targetCurrency = (e.target as HTMLSelectElement).value;
				targetValue = calculateTarget();
			}}
		>
			<option value="usd">USD</option>
			<option value="eur">EUR</option>
			<option value="gbp">GBP</option>
		</select>
	</div>
</div>

<style lang="scss">
	.wrapper {
		font-family: Arial, Helvetica, sans-serif;
		background-color: #131313;
		padding: 20px;
		margin: 20px 10px;
		border-radius: 10px;
		.conversion {
			margin-bottom: 20px;
			span.base {
				opacity: 0.6;
				font-size: 14px;
				display: block;
				margin-bottom: 5px;
			}
			span.target {
				font-size: 28px;
				display: block;
			}
		}
		.base {
			margin-bottom: 15px;
		}
		.base,
		.target {
			select,
			input {
				background-color: transparent;
				color: #fff;
				border: 1px solid rgba(255, 255, 255, 0.1);
				border-radius: 5px;
				padding: 10px;
				&:focus-visible {
					outline: 1px solid rgb(65, 189, 209);
				}
			}
			input {
				&::-webkit-outer-spin-button,
				&::-webkit-inner-spin-button {
					-webkit-appearance: none;
					margin: 0;
				}
			}
		}
	}
</style>
