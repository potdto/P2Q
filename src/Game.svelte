<script>
    import Board from "./Board.svelte";
    import Overlay from "./Overlay.svelte";
    export let level = "Level 1";
    export let closeWindow = () => {};
    export let fen = "start";
    export let winCondition = "capture";
    function win() {
        const locked = JSON.parse(localStorage.getItem("locked"));
        locked[Number(level.split(" ")[1])+1] = false;
        localStorage.setItem("locked", JSON.stringify(locked));
        closeWindow();
    }
</script>

<div on:click={closeWindow}>
    <Overlay />
</div>
<main>
    <span>{level}</span>
    <Board {fen} {win} {winCondition} />
</main>

<style>
    main :global(*) {
        z-index: 11;
    }

    span {
        position: relative;
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        font-weight: 900;
        font-size: 2em;
        color: white;
    }
</style>
