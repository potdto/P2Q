<script>
    import Node from "./Node.svelte";
    export let onNodeClick = () => console.log("clicked");
</script>

<Node
    level="1"
    onClick={onNodeClick}
    position={{ top: 80, left: 10 }}
    img="https://upload.wikimedia.org/wikipedia/commons/8/85/Chess_kll45.svg"
/>
<Node
    level="2"
    onClick={onNodeClick}
    position={{ top: 60, left: 25 }}
    img="https://upload.wikimedia.org/wikipedia/commons/4/44/Chess_rll45.svg"
/>
<Node
    level="3"
    onClick={onNodeClick}
    position={{ top: 70, left: 40 }}
    img="https://upload.wikimedia.org/wikipedia/commons/1/1e/Chess_bll45.svg"
/>
<Node
    level="4"
    onClick={onNodeClick}
    position={{ top: 50, left: 45 }}
    img="https://upload.wikimedia.org/wikipedia/commons/9/9a/Chess_qll45.svg"
/>
<Node
    level="5"
    onClick={onNodeClick}
    position={{ top: 70, left: 70 }}
    img="https://upload.wikimedia.org/wikipedia/commons/a/ad/Chess_nll45.svg"
/>
<Node
    level="6"
    onClick={onNodeClick}
    position={{ top: 60, left: 80 }}
    img="https://upload.wikimedia.org/wikipedia/commons/8/86/Chess_pll45.svg"
/>
<Node
    level="7"
    onClick={onNodeClick}
    position={{ top: 40, left: 60 }}
    img="/img/level7.png"
/>
<Node
    level="8"
    onClick={onNodeClick}
    position={{ top: 25, left: 75 }}
    img="/img/level8.png"
/>
<Node
    level="9"
    onClick={onNodeClick}
    position={{ top: 10, left: 50 }}
    img="/img/level9.png"
/>
<Node
    level="10"
    onClick={onNodeClick}
    position={{ top: 30, left: 15 }}
    img="/img/level10.png"
/>
