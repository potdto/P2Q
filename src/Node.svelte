<script>
    export let level = 1;
    export let img = "http://picsum.photos/400";
    let locked;
    setInterval(() => {
        locked = JSON.parse(localStorage.getItem("locked"))[level];
    });
    export let onClick = () => console.log("click");
    export let position = { top: Math.random() * 90, left: Math.random() * 90 };
</script>

<main
    id={level}
    style="position: absolute; top: {position.top}%; left: {position.left}%"
>
    <div id="wheel" />
    <img
        src={img}
        class="level-img {locked ? 'locked' : ''}"
        alt=""
        on:click={locked
            ? () => {}
            : () =>
                  onClick(
                      document.querySelector(
                          `main[id="${level}"]>label[for=level]`
                      ).innerText
                  )}
    />
    <label for="level">Level {level}</label>
</main>

<style>
    main {
        width: 10%;
    }
    label {
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        font-weight: 900;
        font-size: 100%;
    }
    .level-img {
        width: 40%;
        border-radius: 50%;
        border: 1px solid black;
    }
    .level-img.locked {
        filter: grayscale(100%);
    }
    .level-img:not(.locked):not(.completed) {
        transform: rotate(50deg);
        animation: rotateTo 0.5s;
    }
    .level-img:not(.locked):not(.completed):hover {
        transform: rotate(0deg);
        animation: rotateBack 0.5s;
    }
    .level-img:not(.locked):hover {
        cursor: pointer;
    }
    @keyframes rotateBack {
        from {
            transform: rotate(50deg);
        }
        to {
            transform: rotate(0deg);
        }
    }
    @keyframes rotateTo {
        from {
            transform: rotate(0deg);
        }
        to {
            transform: rotate(50deg);
        }
    }
</style>
