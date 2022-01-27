
<svelte:head>
	<title>Vandertramp Verbs</title>

	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Dongle&display=swap" rel="stylesheet">
</svelte:head>
<script>

	import Vandertramp from "./Vandertramp.svelte";

	const letters = [
		
		{letter: "d", isActive: true, verb: "devenir" ,   canUseAvoir: false},
		{letter: "r", isActive: false, verb: "revenir",   canUseAvoir: false},
		{letter: "m", isActive: false, verb: "mourir",    canUseAvoir: false},
		{letter: "r", isActive: false, verb: "rester",    canUseAvoir: false},
		{letter: "s", isActive: false, verb: "sortir",    canUseAvoir: true},
		{letter: "p", isActive: false, verb: "passer",    canUseAvoir: true},
		{letter: "v", isActive: false, verb: "venir",     canUseAvoir: false},
		{letter: "a", isActive: false, verb: "arriver",   canUseAvoir: false}, 
		{letter: "n", isActive: false, verb: "naître",    canUseAvoir: false}, 
		{letter: "d", isActive: false, verb: "descendre", canUseAvoir: true}, 
		{letter: "e", isActive: false, verb: "entrer",    canUseAvoir: true}, 
		{letter: "r", isActive: false, verb: "rentrer",   canUseAvoir: true}, 
		{letter: "t", isActive: false, verb: "tomber",    canUseAvoir: false}, 
		{letter: "r", isActive: false, verb: "retourner", canUseAvoir: true}, 
		{letter: "a", isActive: false, verb: "aller",     canUseAvoir: false}, 
		{letter: "m", isActive: false, verb: "monter",    canUseAvoir: true}, 
		{letter: "p", isActive: false, verb: "partir",    canUseAvoir: false}];
	
	let textbox;
	let labelText = "Verb:";
	let usingAvoir = false;

	function handleKeyDown(event) {
		if (event.code === "Enter" || event.code === "NumpadEnter") {
			cycle();
		}
	}

	function cycle() {

		for (let i = 0; i < letters.length; i++) {
			if (letters[i].isActive) {

				if (textbox.value.toLowerCase() === letters[i].verb.toLowerCase() && usingAvoir === letters[i].canUseAvoir) {
					labelText = "Verb:";
					textbox.value = "";
					letters[i].isActive = false;
					usingAvoir = false;
					textbox.focus();
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
<div class="container">
	<span>
		{#each letters as letter}
		<Vandertramp letter={letter.letter} isActive={letter.isActive}/>
		{/each}

		</span>
		<label for="verb" class="padded">{labelText}</label>
		<input type="text" id="verb" name="verb" bind:this={textbox} on:keydown="{handleKeyDown}">
		<div>
			Does it use Avoir?
			<label>
				<input type=radio bind:group={usingAvoir} name="yes" value={true}>
				Yes
			</label>
			<label>
				<input type=radio bind:group={usingAvoir} name="yes" value={false}>
				No
			</label>
		</div>
		<div>
			<button class="padded" on:click={cycle}>Check</button>
		</div>
</div>

<style>

	.container {
		height: 100%;
		display: flex;
		flex-direction: column;		
		align-items: center;
		justify-content: center;
	
	}
	 .padded {
		 margin-top: 10px;
		 margin-bottom: 10px;
	 }

	 label, input, div {
		 font-size: 30px;
		 font-family: 'Dongle', sans-serif;
	}
</style>


