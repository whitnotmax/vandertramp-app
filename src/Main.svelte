<script>
import { createEventDispatcher } from "svelte";


	import Vandertramp from "./Vandertramp.svelte";

	const letters = [
		
		{letter: "d", isActive: true, verb: "devenir" ,   canUseAvoir: false , definition: "become"},
		{letter: "r", isActive: false, verb: "revenir",   canUseAvoir: false , definition: "come back"},
		{letter: "m", isActive: false, verb: "mourir",    canUseAvoir: false , definition: "die"},
		{letter: "r", isActive: false, verb: "rester",    canUseAvoir: false , definition: "stay"},
		{letter: "s", isActive: false, verb: "sortir",    canUseAvoir: true  , definition: "go out"},
		{letter: "p", isActive: false, verb: "passer",    canUseAvoir: true  , definition: "move past (something/someone)"},
		{letter: "v", isActive: false, verb: "venir",     canUseAvoir: false , definition: "come"},
		{letter: "a", isActive: false, verb: "arriver",   canUseAvoir: false , definition: "arrive"}, 
		{letter: "n", isActive: false, verb: "naître",    canUseAvoir: false , definition: "be born"}, 
		{letter: "d", isActive: false, verb: "descendre", canUseAvoir: true  , definition: "go down"}, 
		{letter: "e", isActive: false, verb: "entrer",    canUseAvoir: true  , definition: "to enter (for the first time)"}, 
		{letter: "r", isActive: false, verb: "rentrer",   canUseAvoir: true  , definition: "to go home or reenter a building"}, 
		{letter: "t", isActive: false, verb: "tomber",    canUseAvoir: false , definition: "fall"} , 
		{letter: "r", isActive: false, verb: "retourner", canUseAvoir: true  , definition: "return to a place you've been before"}, 
		{letter: "a", isActive: false, verb: "aller",     canUseAvoir: false , definition: "go"}, 
		{letter: "m", isActive: false, verb: "monter",    canUseAvoir: true  , definition: "climb"}, 
		{letter: "p", isActive: false, verb: "partir",    canUseAvoir: false , definition: "leave"}];
	
	let textbox;
	let labelText = "Verb:";
	let definitionText = "";
	let usingAvoir = false;

    const dispatch = createEventDispatcher();
    function dispatchEnd() {
        dispatch("end");
    }

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
                        dispatchEnd();
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

<div class="centered">
    {#each letters as letter}
    <Vandertramp letter={letter.letter} isActive={letter.isActive}/>
    {/each}
</div>

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
    <div class="centered column">
        <button class="green curved small-gap" on:click={cycle}>Check</button>
        <p class="small-gap">{definitionText}</p>
    </div>

    <style>
    label, input, div {
        font-size: 30px;
        font-family: 'Dongle', sans-serif;
        max-width:inherit;
   }

   .small-gap {
		margin: 2px;
	}
   </style>