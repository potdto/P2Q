<script>
    export let fen = "start";
    export let win = () => {};
    export let winCondition = "capture";
    let chess;
    const initChess = () => {
        chess = new Chess(
            fen == "start"
                ? "rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1"
                : fen
        );
    };
    let board;
    const initBoard = () => {
        board = Chessboard("board", {
            position: fen,
            draggable: true,
            onSnapEnd: () => board.position(chess.fen()),
            onDrop: (from, to) => {
                const a = chess.move({ from, to });
                if (a == null) {
                    return "snapback";
                }
                setTimeout(() => {
                    if (chess.turn() == "b") {
                        if (winCondition == "nothing") {
                            const moves = chess.moves();
                            const move = moves[Math.floor(Math.random()*moves.length)];
                            chess.move(move);
                            board.position(chess.fen());
                            return;
                        }
                        if (
                            chess.moves().filter((x) => !x.includes("x"))
                                .length == 1
                        ) {
                            chess.move(chess.moves()[0]);
                            board.position(chess.fen());
                        }
                        for (const move of chess.moves())
                            if (move.includes("=")) {
                                board.position(fen);
                                chess.load(fen);
                            }
                    }
                    for (const move of chess.history()) {
                        if (winCondition == "capture" && move.includes("x")) {
                            win();
                        } else if (winCondition == "pawn2squares") {
                            if (move.includes("4")) win();
                            if (move.includes("3")) {
                                board.position(fen);
                                chess.undo();
                            }
                        } else if (winCondition == "castle") {
                            if (move == "O-O") win();
                            else {
                                board.position(fen);
                                chess.undo();
                            }
                        }
                        if (chess.moves().length == 0) {
                            board.position(fen);
                            chess.load(fen);
                        }
                    }
                }, 100);
            },
        });
    };
</script>

<svelte:head>
    <link
        rel="stylesheet"
        href="https://unpkg.com/@chrisoakman/chessboardjs@1.0.0/dist/chessboard-1.0.0.min.css"
        integrity="sha384-q94+BZtLrkL1/ohfjR8c6L+A6qzNH9R2hBLwyoAfu3i/WCvQjzL2RQJ3uNHDISdU"
        crossorigin="anonymous"
    />
    <script
        src="https://cdnjs.cloudflare.com/ajax/libs/chess.js/0.10.3/chess.min.js"
        on:load={initChess}></script>
    <script src="lib/chessboard.js" on:load={initBoard} defer></script>
</svelte:head>

<div id="board" style="width: 25%; height: 25%" />
