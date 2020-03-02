<script>
 	import { Router, Link, Route } from "svelte-routing";
	import { onMount } from "svelte";
	export let url = "";
    import {push, pop, replace} from 'svelte-spa-router';
	let name = 'Synonym Searcher';
	let src = "images/synonym.jpg";
	let word='';
	let name2 = 'foster';	
	let allSynonyms;
	
	
	const apiURL = "https://www.dictionaryapi.com/api/v3/references/thesaurus/json/{word}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc";


	export const findSynonyms = (async () => {
		const response = await fetch(`https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${word}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc`)
		const data = await response.json();
		const fullSynonyms = data.map(object => {
			return object.meta.syns
		})
		allSynonyms=fullSynonyms[0][0]
	})


	export const findNewSynonym = (async (e) => {
		const newWord = e.target.innerHTML
		const response = await fetch(`https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${newWord}?key=0b203aa3-249e-401e-ab9e-867771f5d1fc`)
		const data = await response.json();
		const fullSynonyms = data.map(object => {
			return object.meta.syns
		})
		allSynonyms=fullSynonyms[0][0]
	})
</script>
<style>
	body {
	}
	span{
		font-weight: bold;	
	}
	main{
		display: flex;
    	flex-direction: column;
    	align-items: center;
		border: solid 1px deepskyblue;
    	background-color: skyblue;	
	}
	h1{
		text-decoration: underline;
		color:tomato;
		margin:10px;
		width:35%;
		text-align:center
	}
	li{
		text-decoration: underline;
		cursor: pointer;
	}
	li:hover,
	li:focus{
			transform: scale(1.05);
	}
	button {
		background-color: tomato;
    	border-radius: 10px;
    	cursor: pointer;
    	width: 210px;
    	height: 50px;
	}
	button:hover,
	button:focus{
			transform: scale(1.05);
	}
	input{
		outline-width: 0;
    	height: 50px;
    	width: 210px;
    	border-radius: 10px;
	}
</style>
<main>
	<h1>{name}!</h1>
	<form>
		<input type ='text' placeholder='Enter Word' bind:value={word}>
	</form>
		<button className ='search-button' on:click={findSynonyms}>
		Search For Synonyms
		</button>
		{#if allSynonyms}
		{#each allSynonyms as synonym}
		<button on:click={findNewSynonym}>{synonym}</button>
	{/each}
		{/if}
	<img {src} alt="background image" />
</main>