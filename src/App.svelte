<script>
	import Vandertramp from "./Vandertramp.svelte";

	const letters = [
		
		{letter: "d", isActive: true, verb: "abc" , canUseEtre: false},
		{letter: "r", isActive: false, verb: "abc", canUseEtre: false},
		{letter: "m", isActive: false, verb: "abc", canUseEtre: false},
		{letter: "r", isActive: false, verb: "abc", canUseEtre: false},
		{letter: "s", isActive: false, verb: "abc", canUseEtre: false},
		{letter: "p", isActive: false, verb: "abc", canUseEtre: false},
		{letter: "v", isActive: false, verb: "abc", canUseEtre: false},
		{letter: "a", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "n", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "d", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "e", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "r", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "t", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "r", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "a", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "m", isActive: false, verb: "abc", canUseEtre: false}, 
		{letter: "p", isActive: false, verb: "abc", canUseEtre: false}];
	
	let labelText = "Verb:";

	function cycle() {
		let found = false;
		const element = document.getElementById("verb");

		for (let i = 0; i < letters.length; i++) {
			if (letters[i].isActive) {

				if (element.value === letters[i].verb) {
					labelText = "Verb:";
					letters[i].isActive = false;
				if (i == letters.length - 1) {
					letters[0].isActive = true;
				} else {
					letters[i + 1].isActive = true;
				}
				break;
				} else {
					labelText = "Incorrect, try again:";
				}
				
			}
		}
		letters = letters;
	}

</script>

{#each letters as letter}
<Vandertramp letter={letter.letter} isActive={letter.isActive} verb={letter.verb} canUseEtre={letter.canUseEtre}/>
{/each}

<label for="verb">{labelText}</label>
<input type="text" id="verb" name="verb">

<div>
	
	<button on:click={cycle}>Check</button>
</div>


