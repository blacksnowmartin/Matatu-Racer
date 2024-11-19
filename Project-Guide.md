### 1. **Game Setup**
   - **Platform:** HTML, CSS, and JavaScript.
   - **Canvas:** Use the `<canvas>` element for drawing the matatu, road, obstacles, and other elements.
   - **Controls:** Arrow keys or swipe gestures for left, right, up, and down.

### 2. **Game Elements**
   - **Matatu Sprite:** Draw or use a simple matatu icon to represent the player's vehicle.
   - **Road & Background:** Draw lanes and add Kenyan-themed obstacles like potholes, pedestrians, and maybe even “Kanjo” (city council officers).
   - **Obstacles:** Randomly generate objects on the road that players must avoid to stay in the game. These could include:
     - Potholes
     - Vendors and pedestrians
     - Traffic barriers
     - “Kanjo” (city council officers)

### 3. **Game Mechanics**
   - **Movement:** Allow players to move left and right to avoid obstacles.
   - **Point System:** Players earn points for every second they avoid an obstacle and get extra points for collecting passengers or tokens that appear on the road.
   - **Collision Detection:** If the matatu hits an obstacle, end the game and display the score.
   - **Speed Increase:** As time progresses, gradually increase the speed of obstacles to make the game more challenging.

### 4. **Basic Code Structure**
Here’s a quick template to get you started:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Matatu Racer</title>
  <style>
    canvas { background: #e0e0e0; display: block; margin: 0 auto; }
    body { text-align: center; font-family: Arial, sans-serif; }
  </style>
</head>
<body>
  <h1>Matatu Racer</h1>
  <canvas id="gameCanvas" width="400" height="600"></canvas>
  <p>Use Arrow Keys to move the Matatu!</p>
  
  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');

    // Create and load the matatu image
    const matatuImg = new Image();
    matatuImg.src = 'matatu.png';

    let matatu = { x: 180, y: 500, width: 38, height: 66 };  // Updated dimensions
    let obstacles = [];
    let score = 0;
    let gameOver = false;

    function drawMatatu() {
        // Replace rectangle with image
        ctx.drawImage(matatuImg, matatu.x, matatu.y, matatu.width, matatu.height);
    }

    function drawObstacles() {
      ctx.fillStyle = "red";
      obstacles.forEach(obs => ctx.fillRect(obs.x, obs.y, obs.width, obs.height));
    }

    function updateObstacles() {
      obstacles.forEach(obs => obs.y += 4);  // increase speed over time
      if (Math.random() < 0.02) {
        obstacles.push({ x: Math.random() * 360, y: 0, width: 40, height: 40 });
      }
      obstacles = obstacles.filter(obs => obs.y < canvas.height);
    }

    function detectCollision() {
      for (let obs of obstacles) {
        if (matatu.x < obs.x + obs.width &&
            matatu.x + matatu.width > obs.x &&
            matatu.y < obs.y + obs.height &&
            matatu.y + matatu.height > obs.y) {
          gameOver = true;
          alert('Game Over! Score: ' + score);
        }
      }
    }

    function gameLoop() {
      if (gameOver) return;

      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawMatatu();
      drawObstacles();
      updateObstacles();
      detectCollision();
      score++;
      requestAnimationFrame(gameLoop);
    }

    document.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowLeft' && matatu.x > 0) matatu.x -= 10;
      if (e.key === 'ArrowRight' && matatu.x < canvas.width - matatu.width) matatu.x += 10;
    });

    gameLoop();
  </script>
</body>
</html>
```

### 5. **Additional Enhancements**
   - **Sound Effects:** Add some matatu music in the background and sound effects for picking up passengers or hitting obstacles.
   - **Score Display:** Show the current score on the screen as the player progresses.
   - **Game Restart:** After game over, allow players to restart the game to beat their previous score.

Let me know if you need help with further customization or if you’re ready to hit the road!

# Blacksnow Martin 2024 
