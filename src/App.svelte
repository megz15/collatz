<script lang="ts">
	import svelteLogo from './assets/svelte.svg'
	import viteLogo from '/vite.svg'
	import Counter from './lib/Counter.svelte'

	let n = 0

    const collatz = () => {
		let collatz_sequence = [n]
		while (n!=1) {			
			if (n%2 == 0) n/=2
			else n = (n*3)+1
			collatz_sequence.push(n)
		}
		alert(collatz_sequence)
	}
</script>

<main>
	<div>
		<a href="https://vitejs.dev" target="_blank" rel="noreferrer">
		<img src={viteLogo} class="logo" alt="Vite Logo" />
		</a>
		<a href="https://svelte.dev" target="_blank" rel="noreferrer">
		<img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
		</a>
	</div>
	<h1>Collatz Conjecture</h1>

	<div class="card">
		<Counter/>
	</div>

	<div class="card">
		Numero: <input placeholder="Enter value" bind:value={n}> <button on:click={collatz}>Enter</button>
	</div>

	<div class="card">
		Made with &lt;3 by <a href="https://github.com/megz15" target="_blank" rel="noreferrer">Meghraj Goswami</a>
	</div>

</main>

<style>
	.logo {
		height: 6em;
		padding: 1.5em;
		will-change: filter;
		transition: filter 300ms;
	}
	.logo:hover {
		filter: drop-shadow(0 0 2em #646cffaa);
	}
	.logo.svelte:hover {
		filter: drop-shadow(0 0 2em #ff3e00aa);
	}
</style>
