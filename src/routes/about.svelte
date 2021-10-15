<script>
	import '../app.css'
</script>

<main>
	<article>
		<h1> The Baselga time transform </h1>
		
		<body>
		
			<p> Sir Baselga is known for being inaccurate. The baselga timer implements a Lorentz-Odilf transfrom (the Lorentz transform being, of course, the equation to correct for Einstein's spacetime dilation) to achieve the most accurate resulting time that current technology can offer.
			<hr>
		
			<p>
				The Lorentz-Odilf transforms incorporates the latests findings of physics, chemestry, geology, biochemestry, biology, botany, zoology and furry science.
			</p>
		
			<button on:click={() => location.href = "/"}> Return </button>
		</body>
	</article>
</main>

<style>

	main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	
	article {
		width: min(30em, 90vw);
	}

	body {
		font-family: "Roboto";
		font-weight: 300;
	}
</style>