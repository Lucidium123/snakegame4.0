var canvas = document.getElementById('game');
var context = canvas.getContext('2d');
var score = 0;
var grid = 16;
var count = 0;
var gameIsOver = false;

var snake = {
  x: 160,
  y: 160,
  dx: grid,
  dy: 0,
  cells: [],
  maxCells: 4
};

var apple = {
  x: 320,
  y: 320
};

function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min)) + min;
}

function loop() {
  requestAnimationFrame(loop);

  // slow game loop to 15 fps instead of 60 (60/15 = 4)
  if (++count < 4) {
    return;
  }

  count = 0;
  context.clearRect(0, 0, canvas.width, canvas.height);

  // Check if the game is over before updating the score
  if (!gameIsOver) {
    // Move this part inside the loop function
    // draw apple
    context.fillStyle = 'red';
    context.fillRect(apple.x, apple.y, grid - 1, grid - 1);

    // move snake by its velocity
    snake.x += snake.dx;
    snake.y += snake.dy;

    // wrap snake position horizontally on the edge of the screen
    if (snake.x < 0) {
      snake.x = canvas.width - grid;
    } else if (snake.x >= canvas.width) {
      snake.x = 0;
    }

    // wrap snake position vertically on the edge of the screen
    if (snake.y < 0) {
      snake.y = canvas.height - grid;
    } else if (snake.y >= canvas.height) {
      snake.y = 0;
    }

    // keep track of where snake has been. the front of the array is always the head
    snake.cells.unshift({ x: snake.x, y: snake.y });

    // remove cells as we move away from them
    if (snake.cells.length > snake.maxCells) {
      snake.cells.pop();
    }

    // draw snake one cell at a time
    context.fillStyle = 'green';
    snake.cells.forEach(function (cell, index) {
      // drawing 1 px smaller than the grid creates a grid effect in the snake body so you can see how long it is
      context.fillRect(cell.x, cell.y, grid - 1, grid - 1);

      // snake ate apple
      if (cell.x === apple.x && cell.y === apple.y) {
        snake.maxCells++;

        // Increase the score
        score++;

        // Update the scoreboard
        document.getElementById('scoreElement').innerHTML = 'Score: ' + score;

        // canvas is 400x400, which is 25x25 grids
        apple.x = getRandomInt(0, 25) * grid;
        apple.y = getRandomInt(0, 25) * grid;
      }

      // check collision with all cells after this one (modified bubble sort)
      for (var i = index + 1; i < snake.cells.length; i++) {
        // snake occupies the same space as a body part. reset the game
        if (cell.x === snake.cells[i].x && cell.y === snake.cells[i].y) {
          gameOver();
          return; // Exit the loop when the game is over
        }
      }
    });
  }
}

// listen to keyboard events to move the snake
document.addEventListener('keydown', function (e) {
  // Arrow keys
  if (e.key === 'ArrowLeft' && snake.dx === 0) {
    snake.dx = -grid;
    snake.dy = 0;
  } else if (e.key === 'ArrowUp' && snake.dy === 0) {
    snake.dy = -grid;
    snake.dx = 0;
  } else if (e.key === 'ArrowRight' && snake.dx === 0) {
    snake.dx = grid;
    snake.dy = 0;
  } else if (e.key === 'ArrowDown' && snake.dy === 0) {
    snake.dy = grid;
    snake.dx = 0;
  }

  // WASD keys
  if (e.key === 'a' && snake.dx === 0) {
    snake.dx = -grid;
    snake.dy = 0;
  } else if (e.key === 'w' && snake.dy === 0) {
    snake.dy = -grid;
    snake.dx = 0;
  } else if (e.key === 'd' && snake.dx === 0) {
    snake.dx = grid;
    snake.dy = 0;
  } else if (e.key === 's' && snake.dy === 0) {
    snake.dy = grid;
    snake.dx = 0;
  }
});

function gameOver() {
  // Handle game-over logic

  // Set the gameIsOver flag to true
  gameIsOver = true;

  // Reset snake position and cells
  snake.x = 160;
  snake.y = 160;
  snake.cells = [];
  snake.maxCells = 4;
  snake.dx = grid;
  snake.dy = 0;

  // Reset apple position
  apple.x = getRandomInt(0, 25) * grid;
  apple.y = getRandomInt(0, 25) * grid;

  // Reset the gameIsOver flag
  gameIsOver = false;

  // Reset the score to 0
  score = 0;

  // Update the score display
  document.getElementById('scoreElement').innerHTML = 'Score: ' + score;
}

// start the game
requestAnimationFrame(loop);
