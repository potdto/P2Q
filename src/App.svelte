<script>
	import Navigation from "./Navigation.svelte";
	import Game from "./Game.svelte";
	import { fade } from "svelte/transition";
	import Dialogue from "./Dialogue.svelte";
	let playing = false;
	let playedBefore = false;
	let level;
	function onNodeClick(a) {
		level = a;
		playing = true;
	}

	if (!localStorage.getItem("locked")) {
		localStorage.setItem(
			"locked",
			"[null, false, true, true, true, true, true, true, true, true, true, true]"
		);
	} else {
		playedBefore = true;
	}

	setInterval(() => {
		const lastElement = document.body.lastChild;
		if (lastElement.src != undefined) {
			lastElement.style.zIndex = "11";
		}
	});
</script>

<svelte:head>
	<script
		src="https://code.jquery.com/jquery-3.5.1.min.js"
		integrity="sha384-ZvpUoO/+PpLXR1lu4jmpXWu80pZlYUAfxl5NsBMWOEPSjUn/6Z/hRTt8+pR6L4N2"
		crossorigin="anonymous"></script>
</svelte:head>

<main>
	{#if !playedBefore}
		<Dialogue
			text="Welcome! Click this text box to continue.&I'm your friend, horsey horse.&I'll explain you the rules of chess.&Click on level 1 to continue..."
		/>
	{/if}
	<Navigation {onNodeClick} />
	{#if playing}
		{#await fetch("/levels.json").then((res) => res.json())}
			&nbsp;
		{:then data}
			<Dialogue {...data[level]} />
			<div transition:fade>
				<Game
					{level}
					closeWindow={() => {
						playing = false;
					}}
					{...data[level]}
				/>
			</div>
		{/await}
	{/if}
</main>

<style>
	main :global(*) {
		text-align: center;
		display: block;
		margin: auto;
		user-select: none;
	}
</style>
