<script>
	let name = 'Synonym Searcher';
	let src = "images/synonym.jpg";
	let word='';
	let newWord='';
	let allSynonyms;
	let input={hasInputted:false}
	
	
	const apiURL = "https://www.dictionaryapi.com/api/v3/references/thesaurus/json/{word}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc";


	export const findSynonyms = (async () => {
		const response = await fetch(`https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${word}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc`)
		const data = await response.json();
		const fullSynonyms = data.map(object => {
			return object.meta.syns
		})
		document.getElementById('myInput').value = ''
		allSynonyms=fullSynonyms[0][0]
	})


	export const findNewSynonym = (async (e) => {
		newWord = e.target.innerHTML
		const response = await fetch(`https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${newWord}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc`)
		const data = await response.json();
		const fullSynonyms = data.map(object => {
			return object.meta.syns
		})
		allSynonyms=fullSynonyms[0][0]
	})

		const handleKeydown = () => {
			input={hasInputted:true}
			console.log(input.value)
	}

</script>

<style>
	main{
		display: flex;
    	flex-direction: column;
    	align-items: center;
		border: solid 1px deepskyblue;
    	background-color: skyblue;	
	}

	span {
  		font-weight: bold;
	}
	h1{
		text-decoration: underline;
		color:tomato;
		margin:10px;
		width:35%;
		text-align:center
	}
	div{
	    justify-content: center;
    	display: flex;
    	flex-flow: row wrap;
    	overflow: auto;
	}
	button {
		background-color: tomato;
    	border-radius: 10px;
    	cursor: pointer;
    	width: 210px;
    	height: 50px;
	}
	button:hover,
	input{
		outline-width: 0;
    	height: 50px;
    	width: 210px;
    	border-radius: 10px;
	}
	.button-results{
		background-color: white;
		border-radius: 10px;
    	cursor: pointer;
    	width: 210px;
    	height: 50px;
	}
	.button-results:hover{
		outline-width: 0;

	}
	p{
		color: navy;
    	font-size: large;
	}
</style>

<main>
	<h1>{name}!</h1>
	<form>
		<input type ='text' placeholder='Enter Word' bind:value={word} id="myInput" on:keydown={handleKeydown}>
	</form>
		<button className ='search-button' on:click={findSynonyms}>
				Search For Synonyms
		</button>
		{#if allSynonyms}
		<p>Results for <span>{newWord.toUpperCase()||word.toUpperCase()}</span></p>
		<div>
			{#each allSynonyms as synonym}
				<button class='button-results'on:click={findNewSynonym}>{synonym}</button>
			{/each}
		</div>
		{/if}
	<img {src} alt="background image" />
</main>