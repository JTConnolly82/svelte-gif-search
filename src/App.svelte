<script>
	// you might export vars to be interpreted by other files/components
	// ex. export let search = blank <-- could be picked up by main.js
	let search = '';
	let loading = false;
	

	const API_URL = 'https://api.giphy.com/v1/gifs/search?api_key=MUGcvgfBd4KBLOycjNTjkQdUArKubDLF&rating=pg&q='

	let gifs = [];

	async function formSubmitted (event) {
		
		event.preventDefault();
		loading = true;
		gifs = [];
		const url= `${API_URL}${search}`
		const response = await fetch(url);
		const json = await response.json();
		gifs = json.data.map(gif => gif.images.fixed_height.url);
		console.log(gifs);
		loading = false;
	}


</script>

<style>
	h1 {
		color: green;
	}
	img {
		border-radius: 8px;
		width: 100%;
		height: auto;
	}
	.results {
		column-count: 3;
	}
	.btn {
		border-radius: 6px;
	
	}
	#search {
		border-radius: 6px;
	}
</style>



{#if (search === '' || !gifs)}
<h3>
	Search for a gif!
</h3>
{/if}


<form on:submit={formSubmitted}>
	<input bind:value={search} id="search" name="search"/>
	<button onmouseover="" style="cursor: pointer;" class='btn' type="submit">Search</button>
</form>

{#if loading && search !== ''}
<h3>Loading...</h3>
{:else}
<div class="results">
	{#each gifs as gif}
	<img alt="gif" src={gif} />
	{/each}
</div>
{/if }



