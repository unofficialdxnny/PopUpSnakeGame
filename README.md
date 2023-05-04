# PopUpSnakeGame
Play this snake game offline on any browser console


### Usage
- Open your browser console <br>
- Copy the below code
```
(function() { // Set up the canvas and game objects var size = 20; var width = 1200; var height = 600; var snake = [{ x: 10, y: 10 }]; var food = { x: 15, y: 15 }; var direction = 'right'; var intervalId; var score = 0; // Create the game window var gameWindow = window.open('', '_blank', 'width=400,height=420'); gameWindow.document.write('<canvas id="canvas"></canvas>'); // Set up the canvas and add it to the game window var canvas = gameWindow.document.getElementById('canvas'); canvas.width = width; canvas.height = height; canvas.style.border = '1px solid black'; // Get the canvas context var ctx = canvas.getContext('2d'); // Start the game loop function startGame() { intervalId = setInterval(function() { update(); draw(); }, 100); } // Update the game state function update() { // Move the snake var head = { x: snake[0].x, y: snake[0].y }; switch (direction) { case 'right': head.x++; break; case 'left': head.x--; break; case 'up': head.y--; break; case 'down': head.y++; break; } snake.unshift(head); // Check for collision with the food if (head.x === food.x && head.y === food.y) { food.x = Math.floor(Math.random() * (width / size)); food.y = Math.floor(Math.random() * (height / size)); score++; } else { snake.pop(); } // Check for collision with the walls if (head.x < 0 || head.x >= width / size || head.y < 0 || head.y >= height / size) { endGame(); } // Check for collision with the snake's body for (var i = 1; i < snake.length; i++) { if (head.x === snake[i].x && head.y === snake[i].y) { endGame(); } } } // Draw the game state function draw() { // Clear the canvas ctx.clearRect(0, 0, width, height); // Draw the food ctx.fillStyle = 'red'; ctx.fillRect(food.x * size, food.y * size, size, size); // Draw the snake ctx.fillStyle = 'green'; snake.forEach(function(segment) { ctx.fillRect(segment.x * size, segment.y * size, size, size); }); // Draw the score ctx.fillStyle = 'black'; ctx.font = '12px Arial'; ctx.fillText('Score: ' + score, 10, height + 15); } // End the game function endGame() { clearInterval(intervalId); gameWindow.alert('Game over! Your score is: ' + score); gameWindow.close(); } // Handle keyboard input document.addEventListener('keydown', function(event) { switch (event.keyCode) { case 37: // left arrow if (direction !== 'right') { direction = 'left'; } break; case 38: // up arrow if (direction !== 'down') { direction = 'up'; } break; case 39: // right arrow if (direction !== 'left') { direction = 'right'; } break; case 40: // down arrow if (direction !== 'up') { direction = 'down'; } break; } }); // Start the game startGame(); })();
```
- Paste it inside the browser console<br>
- Press enter
