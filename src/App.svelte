<script>
	let name = 'Synonym Searcher';
	let src = "images/synonym.jpg";
	let word='';
	let name2 = 'foster';	
	let allSynonyms;
	import SynonymContainer from './SynonymContainer.svelte';
	import { onMount } from "svelte";
	const apiURL = "https://www.dictionaryapi.com/api/v3/references/thesaurus/json/{word}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc";


	const findSynonyms = (async () => {
		const response = await fetch(`https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${word}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc`)
		const data = await response.json();
		const fullSynonyms = data.map(object => {
			return object.meta.syns
		})
		allSynonyms=fullSynonyms[0][0].join()
	})




</script>

	

<style>
	body {
	}
	main{
		display: flex;
    	flex-direction: column;
    	align-items: center;
		
	}
	h1{
		text-decoration: underline;
		color:blue;
		margin:10px;
		width:35%;
	}
	button {
		background-color: grey;
		border-radius:5px;
		cursor:pointer;
		width:35%;
		height:50px
	}
	button:hover,
	button:focus{
			transform: scale(1.05);
	}
	input{
		outline-width: 0;
		height:50px

	}
</style>
<main>
	<h1>Welcome to  {name}!</h1>
	<form>
		<input type ='text' placeholder='Enter Word' bind:value={word}>
	</form>
		<button className ='search-button' on:click={findSynonyms}>
		Search For Synonyms
		</button>
	<img {src} alt="background image" />
	<p>{allSynonyms}</p>
	

</main>