<script>

import { onMount } from "svelte";


let categories = []; 
let difficulties = []; 
let selectedCat = ''; 
let selectedDiff = ''; 
let questions = []; 
let selectedQuestion = ''; 

onMount(() => {
	fetch(`https://opentdb.com/api.php?amount=10`)
	.then(function(response) {
		return response.json()
	})
	.then((data) => {
		console.log(data)
		categories = data.results.category; 
		difficulties = data.results.difficulty; 
		questions = data.results.question; 
	})
})

	
	async function getQuestions() {
		const response = await fetch(`https://opentdb.com/api.php?amount=10&category=${selectedCat}&difficulty=${selectedDiff}`)
		const data = await response.json(); 


	}
	

	let count = 0; 

	function correctAnswer() {
		count += 1;
		console.log(count)
	}
	
	
	function wrongAnswer() {
		count -= 1;
		console.log(count)
	}
	
	
	
	
</script>


<main>
	<h1>Trivia Game</h1>
	
<div>

<label>Choose Category</label>
<select bind:value="{selectedCat}" name="category" id="category">
	<option value="">Please choose an option</option>
	{#each categories as category}
	<option value="{category.id}">{category.name}</option>
	{/each}
	</select>
</div>
<div>
<select bind:value="{selectedDiff}" name="difficulty" id="difficulty">
	  <option disabled selected>Choose Difficulty</option>
	{#each difficulties as difficulty}
    <option value="1">{difficulty.easy}</option>
    <option value="2">{difficulty.medium}</option>
    <option value="3">{difficulty.hard}</option>
	{/each}
	</select>
</div>

<div>
<button on:click={() => getQuestions()}>Start Game!</button>
</div>


<div>
<div>{questions}</div>
<button>Answer 1</button>
<button>Answer 2</button>
<button>Answer 3</button>
<button>Answer 4</button>
</div>


</main>


