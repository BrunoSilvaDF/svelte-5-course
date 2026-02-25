<script lang="ts">
	const target = {
		firstName: 'Bruno',
		lastName: 'Santos',
		occupations: [],
		set occupation(value: string) {
			this.occupations.push(value);
		},
		get fullName() {
			return `${this.firstName} ${this.lastName}`;
		}
	};

	const proxy = new Proxy(target, {
		get(target, prop) {
			// console.log('target, prop :>> ', target, prop);
			return prop in target ? target[prop as keyof typeof target] : 'Nah';
		},
		set(target, prop, value) {
			console.log('target, prop, value :>> ', target, prop, value);
			target[prop] = value;
			return true;
		}
	});

	console.log(proxy.firstnamess);
</script>

hau

<style>
	:global {
		body {
			background-color: #222;
		}
	}
</style>
