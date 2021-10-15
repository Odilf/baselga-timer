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

		return (hours < 10 ? "0" : "") + hours.toFixed(0) + ":" + (minutes < 10 ? "0" : "") + minutes.toFixed(0)
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

	<section>
		<h2> Tiempo baselguiano </h2>
		<input type="time" bind:value={btime}/>
	</section>

	<section>
		<h2> "Llego a las..." </h2>
		<input type="time" bind:value={imat}/>
	</section>

	<section>
		<h2> Tiempo real </h2>
		<h1> {lorentzOdilfTransform(btime, imat, mood)} </h1>
	</section>

	<section>
		<h2> Mood de baselga </h2>
		<input type="range" min=0 max=1 step=0.001 bind:value={mood}/>
		{(mood * 10).toFixed(2)} / 10
	</section>
</main>

<style>
	h1, h2 {
		margin: 1em;

		display: flex;
		justify-content: center;
		align-items: center;
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

		background-color: var(--caca);
	}

	section {
		display: flex;
		/* flex-direction: column; */
		justify-content: center;
		align-items: center;	
	}

	input {
		/* margin: 1em; */
		font-size: 2em;
	}
</style>