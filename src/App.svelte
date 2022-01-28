
<svelte:head>
	<title>Vandertramp Verbs</title>

	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Dongle&display=swap" rel="stylesheet">
</svelte:head>
<script>

	import Vandertramp from "./Vandertramp.svelte";

	const letters = [
		
		{letter: "d", isActive: true, verb: "devenir" ,   canUseAvoir: false , definition: "abc"},
		{letter: "r", isActive: false, verb: "revenir",   canUseAvoir: false , definition: "abc"},
		{letter: "m", isActive: false, verb: "mourir",    canUseAvoir: false , definition: "abc"},
		{letter: "r", isActive: false, verb: "rester",    canUseAvoir: false , definition: "abc"},
		{letter: "s", isActive: false, verb: "sortir",    canUseAvoir: true  , definition: "abc"},
		{letter: "p", isActive: false, verb: "passer",    canUseAvoir: true  , definition: "abc"},
		{letter: "v", isActive: false, verb: "venir",     canUseAvoir: false , definition: "abc"},
		{letter: "a", isActive: false, verb: "arriver",   canUseAvoir: false , definition: "abc"}, 
		{letter: "n", isActive: false, verb: "naître",    canUseAvoir: false , definition: "abc"}, 
		{letter: "d", isActive: false, verb: "descendre", canUseAvoir: true  , definition: "abc"}, 
		{letter: "e", isActive: false, verb: "entrer",    canUseAvoir: true  , definition: "abc"}, 
		{letter: "r", isActive: false, verb: "rentrer",   canUseAvoir: true  , definition: "abc"}, 
		{letter: "t", isActive: false, verb: "tomber",    canUseAvoir: false , definition: "abc"} , 
		{letter: "r", isActive: false, verb: "retourner", canUseAvoir: true  , definition: "abc"}, 
		{letter: "a", isActive: false, verb: "aller",     canUseAvoir: false , definition: "abc"}, 
		{letter: "m", isActive: false, verb: "monter",    canUseAvoir: true  , definition: "abc"}, 
		{letter: "p", isActive: false, verb: "partir",    canUseAvoir: false , definition: "abc"}];
	
	let textbox;
	let labelText = "Verb:";
	let definitionText = "";
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
					definitionText = "";
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
					definitionText = letters[i].definition;
				}
				
			}
		}
		letters = letters;
	}

</script>

<svelte:body on:keydown={handleKeyDown}></svelte:body>

<div class="container centered column">
	<div class="white curved padded">
		<span>
			{#each letters as letter}
			<Vandertramp letter={letter.letter} isActive={letter.isActive}/>
			{/each}
	
		</span>

			<label for="verb">{labelText}</label>
			<input type="text" class="curved" id="verb" name="verb" bind:this={textbox}>
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
			<span class="centered column">
				<button class="green curved small-gap" on:click={cycle}>Check</button>
				<p class="small-gap">{definitionText}</p>
			</span>
	</div>
</div>

<style>
	:global(body) {
		background-color: lightgray;
	}
	.container {
		height: 100%;	
	}

	.small-gap {
		margin: 2px;
	}

	.centered {
		display: flex;
		
		align-items: center;
		justify-content: center;
	}

	.column {
		flex-direction: column;		
	}

	.white {
		background-color: rgba(255, 255, 255, 0.863);
	}

	.green {
		background-color: rgb(31, 153, 0);
	}

	.curved {
		border-radius: 5px;
	}

	 .padded {
		 padding: 20px;
	 }

	 label, input, div {
		 font-size: 30px;
		 font-family: 'Dongle', sans-serif;
	}
</style>


