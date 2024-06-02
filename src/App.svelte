<script lang="ts">
    import { LineChart } from 'chartist'
	import { onMount } from 'svelte'

	let n:number
	let collatz_sequence: number[] = []
	let chart: LineChart;

    const collatz = () => {
		collatz_sequence = [n]
		while (n!=1) {			
			if (n%2 == 0) n/=2
			else n = (n*3)+1
			collatz_sequence.push(n)
		}
		n = collatz_sequence[0]

		chart.update({
			labels: collatz_sequence.map((_, i) => i+1),
			series: [collatz_sequence]
		})
	}

	onMount(() => {
		chart = new LineChart(
			'#chart',
			{
				labels: [],
				series: [[]]
			}
		)
	})

</script>

<main>
	<h1>Collatz Conjecture</h1>

	<div class="card">
		Numero: <input placeholder="Enter value" bind:value={n}> <button on:click={collatz}>Enter</button>
	</div>

	<div id="chart"></div>

	<div class="card">
		<table>
			<tr>
				<th>n</th>
				<th>x<sub>n</sub></th>
			</tr>
			{#each collatz_sequence as n,i}
				<tr>
					<td align="left">{i+1}</td>
					<td align="right">{n}</td>
				</tr>
			{/each}
		</table>
	</div>

	<div class="card">
		Made with &lt;3 by <a href="https://github.com/megz15" target="_blank" rel="noreferrer">Meghraj Goswami</a>
	</div>

</main>