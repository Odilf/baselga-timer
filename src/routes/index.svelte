<script lang="ts">
	import '../app.css'

	let btime = "00:00" // Baselguian time
	let imat: string // "Im at"
	let mood = 0.5

	const max_delay = 30

	function getMins(time: string) {
		return parseInt(time.substr(3, 2)) + parseInt(time.substr(0, 2)) * 60
	}

	function formatTime(inmins: number) {
		let hours = Math.floor(inmins / 60)
		let minutes = inmins % 60

		return (Math.round(hours) >= 10 ? "" : "0") + hours.toFixed(0) + ":" + (Math.round(minutes) >= 10 ? "" : "0") + minutes.toFixed(0)
	}

	function lorentzOdilfTransform(btime: string, imat: string, mood: number) {
		let real = getMins(btime)

		if (imat) {
			let imatm = getMins(imat)
			const delta = imatm - real
			real = imatm + delta
		}

		real += max_delay * (1 - mood)

		return formatTime(real)
	}
</script>

<main>
	<h1> Transformada de Lorentz-Odilf </h1>
	<body>

		<h2> Tiempo baselguiano </h2>
		<input type="time" bind:value={btime}/>

		<h2> "Llego a las..." </h2>
		<input type="time" bind:value={imat}/>
			
		<h2> Tiempo real </h2>
		<h1 class=time> {lorentzOdilfTransform(btime, imat, mood)} </h1>
		
		<h2> Mood de baselga </h2>
		<section>
			<input type="range" min=0 max=0.999 step=0.001 bind:value={mood}/>
			{(mood * 10).toFixed(2)} / 10
		</section>

	</body>

	<button on:click={() => location.href = "/about"}>?</button>
</main>

<style>
	@import "@fontsource/roboto-mono/100.css"; 
	@import "@fontsource/roboto/900.css"; 

	h1, h2 {
		margin: 1em;

		display: flex;
		/* justify-content: center; */
		align-items: center;
	}

	.time {
		display: flex;
		justify-content: center;
		align-items: center;
		
		font-weight: 900;
	}

	h2 {
		font-weight: 100;
	}

	main {
		position: absolute;
		inset: 0;

		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	body {
		display: grid;
		grid-template-columns: 2fr 1fr;
		gap: 10px;
		grid-auto-rows: minmax(100px, auto);
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
	}

	button {
		border-radius: 20%;
		height: 3em;
		width: 3em;
	}
</style>