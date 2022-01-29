
<svelte:head>
	<title>Vandertramp Verbs</title>

	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Dongle&display=swap" rel="stylesheet">
</svelte:head>

<script>
	import Main from "./Main.svelte";

	let isPlaying = false;

	function togglePlaying() {
		isPlaying = !isPlaying;
		console.log(isPlaying);
	}
</script>

<div class="container centered column">
	
		{#if isPlaying}
		<div class="white curved padded">
			<Main on:end={togglePlaying}/>
		</div>

		{:else}
		<button class="green centered curved small-gap" on:click={togglePlaying}>Play</button>
		{/if}
</div>

<style>
	:global(body) {
		background-color: lightgray;
	}
	.container {
		height: 100%;	
	}

	

	:global(.centered) {
		display: flex;
		
		align-items: center;
		justify-content: center;
	}

	:global(.column) {
		flex-direction: column;		
	}

	:global(.white) {
		background-color: rgba(255, 255, 255, 0.863);
		max-width: 60vw;
	}

	

	:global(.green) {
		background-color: rgb(31, 153, 0);
	}

	:global(.curved) {
		border-radius: 5px;
	}

	 :global(.padded) {
		padding: 20px;
	 }

	 button {
		font-size: 30px;
        font-family: 'Dongle', sans-serif;
	 }

</style>


