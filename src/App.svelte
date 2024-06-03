<script lang="ts">
	import { onMount } from 'svelte';
    import { Chart } from 'chart.js/auto';
	import collatz_img from './assets/collatz.svg';

	let n:number
	let collatz_sequence: number[] = []

	let chart: Chart;
  	let chartCanvas: HTMLCanvasElement;

    const calculate = () => {
		collatz_sequence = [n]
		while (n!=1) {			
			if (n%2 == 0) n/=2
			else n = (n*3)+1
			collatz_sequence.push(n)
		}
		n = collatz_sequence[0]
		updateChart()
	}

	onMount(() => {
		chart = new Chart(chartCanvas, {
		type: 'line',
		data: {
			labels: [],
			datasets: [
			{
				label: 'Collatz Sequence Value',
				data: [],
				tension: 0.2
			}
			]
		},
		options: {
			plugins: {
				legend: {
					display: false
				},
			},
			scales: {
			x: {
				beginAtZero: true,
				title: {
					display: true,
					text: 'Index',
					color: "#fff"
				}, ticks: {
					color: "#fff"
				}
			},
			y: {
				beginAtZero: true,
				title: {
					display: true,
					text: 'Value',
					color: "#fff"
				}, ticks: {
					color: "#fff"
				}
			}
			}
		}
		});
	});

	const updateChart = () => {
		if (chart) {
		chart.data.labels = collatz_sequence.map((_, index) => index + 1);
		chart.data.datasets[0].data = collatz_sequence;
		chart.update();
		}
	};

</script>

<main>
	<h1>Collatz Conjecture</h1>
	<img src={collatz_img} style="filter: invert(1);" />
	<!-- <p><a href="https://en.wikipedia.org/wiki/Collatz_conjecture">Read More</a></p> -->

	<div class="card">
		<input placeholder="Value" bind:value={n} size="10"> <button on:click={calculate}>Enter</button>
	</div>

	<div class="card">
		<canvas bind:this={chartCanvas} />
	</div>

	<div class="card">
		<table align="center">
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

	<footer>
		Made with &lt;3 by <a href="https://github.com/megz15" target="_blank" rel="noreferrer">Meghraj Goswami</a>
	</footer>

</main>