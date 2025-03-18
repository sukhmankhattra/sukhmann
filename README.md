# sukhmann
# 🌟 Bouncy Beak

## 📌 Description
Bouncy Beak is a simple yet addictive game where players guide a bird through a series of pipes by tapping the screen to keep it airborne. Its charm lies in its challenging nature and retro-style graphics.

## 🎨 Demo Preview (HTML, CSS & JS)
Here is a simple **HTML, CSS & JavaScript** snippet from the project:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bouncy Beak</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: #f0f0f0;
        }
        canvas {
            border: 1px solid black;
            background: lightblue;
        }
    </style>
</head>
<body>
<canvas id="gameCanvas"></canvas>

<script>
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");

    let canvasWidth = window.innerWidth * 0.6;
    let canvasHeight = window.innerHeight * 0.8;
    canvas.width = canvasWidth;
    canvas.height = canvasHeight;

    let bird, pipes, score, gameOver;

    function resetGame() {
        bird = { 
            x: canvasWidth * 0.1, 
            y: canvasHeight * 0.5, 
            width: 20, 
            height: 20, 
            velocity: 0, 
            gravity: 0.4, 
            jump: -7 
        };
        pipes = [];
        score = 0;
        gameOver = false;
        createPipe();
    }

    function createPipe() {
        const pipeHeight = Math.random() * canvasHeight * 0.5 + 50;
        const gap = canvasHeight * 0.2;
        pipes.push({
            x: canvasWidth,
            top: pipeHeight,
            bottom: canvasHeight - pipeHeight - gap,
            width: 50,
        });
    }

    function drawBird() {
        ctx.fillStyle = "yellow";
        ctx.fillRect(bird.x, bird.y, bird.width, bird.height);
    }

    function drawPipes() {
        ctx.fillStyle = "green";
        pipes.forEach(pipe => {
            ctx.fillRect(pipe.x, 0, pipe.width, pipe.top);
            ctx.fillRect(pipe.x, canvas.height - pipe.bottom, pipe.width, pipe.bottom);
        });
    }

    function update() {
        if (gameOver) return;

        bird.velocity += bird.gravity;
        bird.y += bird.velocity;
        pipes.forEach(pipe => pipe.x -= 2);

        if (pipes[0] && pipes[0].x < -pipes[0].width) {
            pipes.shift();
            score++;
            createPipe();
        }

        pipes.forEach(pipe => {
            if (
                bird.x < pipe.x + pipe.width &&
                bird.x + bird.width > pipe.x &&
                (bird.y < pipe.top || bird.y + bird.height > canvasHeight - pipe.bottom)
            ) {
                gameOver = true;
            }
        });

        if (bird.y + bird.height > canvasHeight || bird.y < 0) gameOver = true;

        ctx.clearRect(0, 0, canvasWidth, canvasHeight);
        drawBird();
        drawPipes();

        ctx.fillStyle = "black";
        ctx.font = "20px Arial";
        ctx.fillText(`Score: ${score}`, 10, 20);

        if (gameOver) {
            ctx.fillStyle = "red";
            ctx.font = "30px Arial";
            ctx.fillText("Game Over! Press Space to Retry", canvasWidth / 4, canvasHeight / 2);
        }
    }

    function jump() {
        if (!gameOver) {
            bird.velocity = bird.jump;
        }
    }

    function retry(event) {
        if (event.code === "Space") {
            if (gameOver) {
                resetGame();
            } else {
                jump();
            }
        }
    }

    function resizeCanvas() {
        canvasWidth = window.innerWidth * 0.6;
        canvasHeight = window.innerHeight * 0.8;
        canvas.width = canvasWidth;
        canvas.height = canvasHeight;
        resetGame();
    }

    window.addEventListener("keydown", retry);
    window.addEventListener("resize", resizeCanvas);

    resetGame();
    setInterval(update, 20);
</script>
</body>
</html>
```

📌 **Output Preview:** This code creates a simple browser game where a bird moves through obstacles.

## 🔹 Features
- 🖼️ Beautiful UI with simple HTML, CSS, and JavaScript.
- 🚀 Responsive gameplay.
- 🛠️ Challenging and addictive.

## 🚀 How to Run the Project
1. Clone the repository:
    ```bash
    git clone https://github.com/sukhmankhattra/sukhmann.git
    ```
2. Navigate to the project directory:
    ```bash
    cd sukhmann
    ```
3. Open `index.html` in a browser to play the game.

## 🤝 Contribution Guidelines
1. Fork the repository.
2. Create a new branch:
    ```bash
    git checkout -b feature-branch
    ```
3. Make your changes and commit them:
    ```bash
    git commit -m "Add new feature"
    ```
4. Push to GitHub and create a Pull Request.

## 📜 License
This project is licensed under the MIT License.

## 👥 Team & Contributors
- Your Name
- Contributor Name

