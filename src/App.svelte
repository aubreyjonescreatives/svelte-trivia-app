<script>
import { onMount } from "svelte";





  let users = [];

  onMount(async () => {
    const res = await fetch(`https://opentdb.com/api.php?amount=10`);
     users = await res.json();
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
    <option value="1">{users.category}</option>
    <option value="2">{users.category}</option>
    <option value="3">{users.category}</option>
	</select>
<select>
	  <option disabled selected>Choose Difficulty</option>
    <option value="1">{users.difficulty}</option>
    <option value="2">{users.difficulty}</option>
    <option value="3">{users.difficulty}</option>
	</select>
	 {#each users as user}
	<ul>
<h1 id="question">{user.question}</h1>
<button on:click={correctAnswer} id="correct_answer">{user.correct_answer}</button>
<li><button on:click={wrongAnswer} id="incorrect_answers">{user.incorrect_answers}</button></li>		
	</ul>
 {/each}
	</form>
</main>


