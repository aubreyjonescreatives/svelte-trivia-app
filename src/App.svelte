<script>
import { onMount } from "svelte";





  let results = [];

  onMount(async () => {
    const res = await fetch(`https://opentdb.com/api.php?amount=10`);
     results = await res.json();
  });

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
	
	
<form>
<select>
  <option disabled selected>Choose Category</option>
    <option value="1">{results.category}</option>
    <option value="2">{results.category}</option>
    <option value="3">{results.category}</option>
	</select>
<select>
	  <option disabled selected>Choose Difficulty</option>
    <option value="1">{results.difficulty}</option>
    <option value="2">{results.difficulty}</option>
    <option value="3">{results.difficulty}</option>
	</select>
	 {#each results as result}
	<ul>
<h1 id="question">{result.question}</h1>
<button on:click={correctAnswer} id="correct_answer">{result.correct_answer}</button>
<li><button on:click={wrongAnswer} id="incorrect_answers">{result.incorrect_answers}</button></li>		
	</ul>
 {/each}
	</form>
</main>


