<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flappy Bird</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #70c5ce;
            font-family: Arial, sans-serif;
        }
        canvas {
            border: 2px solid #000;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="320" height="480"></canvas>

    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // Game Variables
        let bird = { x: 50, y: 150, width: 20, height: 20, gravity: 0.6, lift: -10, velocity: 0 };
        let pipes = [];
        let pipeWidth = 40;
        let pipeGap = 100;
        let score = 0;
        let gameOver = false;

        function drawBird() {
            ctx.fillStyle = "#ffeb3b";
            ctx.fillRect(bird.x, bird.y, bird.width, bird.height);
        }

        function drawPipes() {
            ctx.fillStyle = "#4caf50";
            pipes.forEach(pipe => {
                ctx.fillRect(pipe.x, 0, pipeWidth, pipe.top);
                ctx.fillRect(pipe.x, canvas.height - pipe.bottom, pipeWidth, pipe.bottom);
            });
        }

        function drawScore() {
            ctx.fillStyle = "#fff";
            ctx.font = "20px Arial";
            ctx.fillText("Score: " + score, 10, 30);
        }

        function updateBird() {
            bird.velocity += bird.gravity;
            bird.y += bird.velocity;

            if (bird.y + bird.height >= canvas.height) {
                gameOver = true;
            }

            if (bird.y <= 0) {
                bird.y = 0;
                bird.velocity = 0;
            }
        }

        function updatePipes() {
            if (frames % 90 === 0) {
                let topPipeHeight = Math.floor(Math.random() * (canvas.height - pipeGap - 50)) + 50;
                pipes.push({
                    x: canvas.width,
                    top: topPipeHeight,
                    bottom: canvas.height - (topPipeHeight + pipeGap),
                });
            }

            pipes.forEach((pipe, index) => {
                pipe.x -= 2;

                // Detect collision
                if (
                    bird.x < pipe.x + pipeWidth &&
                    bird.x + bird.width > pipe.x &&
                    (bird.y < pipe.top || bird.y + bird.height > canvas.height - pipe.bottom)
                ) {
                    gameOver = true;
                }

                // Remove pipe if it's out of screen
                if (pipe.x + pipeWidth < 0) {
                    pipes.splice(index, 1);
                    score++;
                }
            });
        }

        function resetGame() {
            bird.y = 150;
            bird.velocity = 0;
            pipes = [];
            score = 0;
            gameOver = false;
        }

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            drawBird();
            drawPipes();
            drawScore();

            if (gameOver) {
                ctx.fillStyle = "#fff";
                ctx.font = "30px Arial";
                ctx.fillText("Game Over", canvas.width / 2 - 70, canvas.height / 2);
                ctx.font = "20px Arial";
                ctx.fillText("Click to Restart", canvas.width / 2 - 70, canvas.height / 2 + 30);
                return;
            }

            updateBird();
            updatePipes();
            frames++;

            requestAnimationFrame(gameLoop);
        }

        canvas.addEventListener("click", function () {
            if (gameOver) {
                resetGame();
                gameLoop();
            } else {
                bird.velocity = bird.lift;
            }
        });

        let frames = 0;
        gameLoop();
    </script>
</body>
</html>
