<script>
	/* import { onMount } from 'svelte' */
	import MovieItem from './Movie/Item.svelte'

	const APIKEY = 'introduzca aqui la API KEY'
	const BASEURL = 'https://api.themoviedb.org/3'
	const APISETTINGS = `?api_key=${APIKEY}&language=es-MX`

	/* let movies = []

	function fetchMovies() {
		const URL = `${BASEURL}/discover/movie${APISETTINGS}&sort_by=popularity.desc`

		fetch(URL)
			.then(res => res.json())
			.then(({results}) => {
				movies = results

				{console.log(results);}
			})
	} */

	const movies = (async() => {
		const URL = `${BASEURL}/discover/movie${APISETTINGS}&sort_by=popularity.desc`
		const response = await fetch(URL)
		
		return await response.json()
	})()
	/* onMount(() => {
		console.log('montado')
		fetchMovies()
	}) */
</script>

<svelte:head>
	<title>Películas</title>
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
</svelte:head>

<main class="container">
	<h1>Películas</h1>
	<p>usando APIs de themoviedb.org</p>
	<div class="row">
		<!-- {#each movies as movie}
			<div class="col-12 col-md-6 col-lg-3 p-2">
				<MovieItem {...movie}/>
			</div>	
		{/each} -->

		{#await movies}
			<p>Cargando...</p>
		{:then data}
			{#each data.results as movie}
				<div class="col-12 col-md-6 col-lg-3 p-2">
					<MovieItem {...movie}/>
				</div>
			{/each}
		{/await}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>