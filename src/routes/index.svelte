<script lang="ts">
import { get } from 'svelte/store';

	import '../app.css'

	let btime = new Date().getHours() + ":" + new Date().getMinutes() // Baselguian time
	let imat: string // "Im at"
	let mood = 0.5

	let reason_val = reason()

	function getMins(time: string): number {
		return parseInt(time.substr(3, 2)) + parseInt(time.substr(0, 2)) * 60
	}

	function formatTime(inmins: number): string {
		let hours = Math.floor(inmins / 60)
		hours = hours % 24
		let minutes = inmins % 60

		return (Math.round(hours) >= 10 ? "" : "0") + hours.toFixed(0) + ":" + (Math.round(minutes) >= 10 ? "" : "0") + minutes.toFixed(0)
	}

	function lorentzOdilfTransform(btime: string, imat: string, mood: number, max_delay = 60): string {
		let real = getMins(btime)

		let delta = 0
		if (imat) {
			let imatm = getMins(imat)
			delta = imatm - real
		}

		console.log(1 - mood);

		const mood_weight = x => 1/(x + 0.1) - 0.9

		real = (real + 2*delta) * 1.01 + max_delay * mood_weight(mood)

		return formatTime(real)
	}

	function reason() {
		const verbs = [
			"he perdido",
			"me ha saltado",
			"ha llegado tarde",
			"ha llegado tarde",
			"ha tenido retrasos",
		]

		const vehicles = [
			"el bus",
			"el bus",
			"el tren",
			"el tren",
			"el metro",
			"el metro",
			"mi padre",
			"mi madre",
		]
		return `"esq ${random(verbs)} ${random(vehicles)}"	`
	}

	function random(list: unknown[]) {
		return list[Math.floor(Math.random()*list.length)]
	}
</script>

<main>
	<h1> Lorentz-Odilf transform for Baselguian Times </h1>
	<body>

		<h2> Tiempo baselguiano </h2>
		<input type="time" bind:value={btime}/>

		<h2> "Llego a las..." </h2>
		<input type="time" bind:value={imat}/>
			
		<h2> Mood de baselga </h2>
		<section>
			<input type="range" min=0 max=1 step=0.001 bind:value={mood}/>
			{(mood * 10).toFixed(2)} / 10
		</section>

		<h2> Tiempo real </h2>
		<h1 class=time> {lorentzOdilfTransform(btime, imat, mood)} </h1>

		<h2> Razón
			<button class=reason on:click={() => reason_val = reason()}> 
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M13.5 2c-5.621 0-10.211 4.443-10.475 10h-3.025l5 6.625 5-6.625h-2.975c.257-3.351 3.06-6 6.475-6 3.584 0 6.5 2.916 6.5 6.5s-2.916 6.5-6.5 6.5c-1.863 0-3.542-.793-4.728-2.053l-2.427 3.216c1.877 1.754 4.389 2.837 7.155 2.837 5.79 0 10.5-4.71 10.5-10.5s-4.71-10.5-10.5-10.5z"/></svg> 
			</button> 
		</h2>
		<p> 
			{reason_val} 
		</p>
		

	</body>

	<button on:click={() => location.href = "/about"}>?</button>
</main>

<style>
	@import "@fontsource/roboto-mono/100.css"; 
	@import "@fontsource/roboto/900.css"; 

	h1, h2 {
		margin: 1rem;

		display: flex;
		/* justify-content: center; */
		align-items: center;
	}

	.time {
		display: flex;
		justify-content: center;
		align-items: center;
		
		font-weight: 900;
		font-size: 3.5rem;
		/* background-color: hsla(0, 100, 20, 20); */
		/* background-color: hsla(0, 100%, 20%, 20%); */
	}

	h2 {
		font-weight: 100;
	}

	main {
		min-width: 100vw;
		min-height: 100vh;
		
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		
		padding-bottom: 5em;
		
	}
	
	body {
		display: grid;
		grid-template-columns: 2fr 1fr;
		gap: 10px;
		grid-auto-rows: minmax(100px, auto);
		/* grid-auto-rows: 100px; */
		width: min(30em, 90vw);
	}

	input {
		/* margin: 1em; */
		font-size: 2em;
		font-family: "Roboto Mono";
		font-weight: 100;
	}

	section {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}

	button {
		border-radius: 20%;
		height: 4em;
		width: 4em;
	}

	p {
		display: flex;
		align-items: center;
		text-align: center;
	}

	
</style>