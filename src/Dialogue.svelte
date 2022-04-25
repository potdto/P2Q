<script>
    import Overlay from "./Overlay.svelte";

    export let text = "test dialogue&testing...&...";
    export let img = "http://picsum.photos/400";
    let uniqueId = Math.random();

    let chunks = text.split("&");
    let chunkIndex = 0;
    function advanceText() {
        if (chunks[++chunkIndex] == undefined) return closeDialogue();

        if (chunks[chunkIndex].includes("%")) {
            document.querySelector(
                `main[id="${uniqueId}"]>.explain-img`
            ).style.display = "block";
            chunks[chunkIndex] = chunks[chunkIndex].replace("%", "");
        }
    }
    function closeDialogue() {
        document.querySelector(
            `main[id="${uniqueId}"].dialogue`
        ).style.display = "none";
    }
</script>

<main class="dialogue" id={uniqueId}>
    <img src={img} alt="" class="explain-img" />
    <img
        src="https://lichess1.org/assets/_veMyGm/piece/horsey/wN.svg"
        alt=""
        class="horsey"
    />
    <span class="msg-box" on:click={advanceText}>{chunks[chunkIndex]}</span>
    <Overlay zIndex="100" />
</main>

<style>
    main {
        position: absolute;
        bottom: 0;
        left: 0;
    }
    main :global(*) {
        position: relative;
        display: inline;
        z-index: 101;
    }
    img {
        width: 40vh;
        height: 40vh;
    }
    .msg-box {
        position: inherit;
        width: 60vw;
        height: 40vh;
        background-color: grey;
        border-radius: 5px;
        font-size: 2em;
    }
    .msg-box:hover {
        cursor: pointer;
    }
    .explain-img {
        position: fixed;
        left: 40vw;
        top: 0;
        display: none;
        margin: 10px;
        border-radius: 5px;
    }
</style>
