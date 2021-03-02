<script>

import { onMount } from "svelte";


let categories = []; 
let difficulties = []; 
let selectedCat = ''; 
let selectedDiff = ''; 
let questions = []; 
let selectedQuestion = ''; 
let correctAnswer = [];  
let incorrectAnswers = [];  

onMount(() => {
	fetch(`https://opentdb.com/api.php?amount=10`)
	.then(function(response) {
		return response.json()
	})
	.then((data) => {
		console.log(data)
		categories = data.results[0].category; 
		difficulties = data.results[0].difficulty; 
		
	})
})

	
	async function getQuestions() {
		const response = await fetch(`https://opentdb.com/api.php?amount=10&category=${selectedCat}&difficulty=${selectedDiff}`)
		const data = await response.json(); 
		
		.then((data) => {
		questions = data.results[0].question; 
		correctAnswer = data.results[0].correct_answer; 
		incorrectAnswers = data.results[0].incorrect_answers; 


		})
	
	}
	

	let count = 0; 

	function rightAnswer() {
		count += 1;
		console.log(count++)
	}
	
	
	function wrongAnswer() {
		count -= 1;
		console.log(count--)
	}
	
	
	
	
</script>


<main>
	<h1>Trivia Game</h1>
	
<div>

<label>Choose Category</label>
<select bind:value="{selectedCat}" name="category" id="category">
	<option disabled selected>Please choose an option</option>
	<option>{categories}</option>
	</select>
</div>
<div>
<label>Choose Difficulty</label>
<select bind:value="{selectedDiff}" name="difficulty" id="difficulty">
	  <option disabled selected>Choose Difficulty</option>
    <option>{difficulties}</option>
	</select>
</div>

<div>
<button on:click={() => getQuestions()}>Start Game!</button>
</div>


<div>
<div>{questions}</div>
<button on:click={() => rightAnswer()}>{correctAnswer}</button>
<button on:click={() => wrongAnswer()}>{incorrectAnswers[0]}</button>
<button on:click={() => wrongAnswer()}>{incorrectAnswers[1]}</button>
<button on:click={() => wrongAnswer()}>{incorrectAnswers[2]}</button>
</div>


</main>


