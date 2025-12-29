
# Snake Game — Python (Pygame)

## Overview
This project is a fully functional Snake Game implemented in Python using the Pygame framework.
It demonstrates core programming concepts such as real-time game loops, event handling, collision detection, and state management.

The project was developed as a foundational software engineering exercise with emphasis on clean structure, readability, and correct game logic, making it suitable for portfolio and technical review.

---

## Features
- Real-time keyboard input handling
- Dynamic snake movement and growth logic
- Collision detection (walls and self)
- Score tracking system
- Game-over state handling
- Structured game loop with frame rate control

---

## Technical Stack
- **Language:** Python 3
- **Framework:** Pygame
- **Paradigm:** Event-driven programming

---

## Project Structure
import pygame
import random

# Initialize pygame
pygame.init()

# Screen size
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Snake Game")

# Colors
COLOR_WHITE = (255, 255, 255)
COLOR_BLACK = (0, 0, 0)
COLOR_RED = (200, 0, 0)
COLOR_GREEN = (0, 200, 0)
COLOR_BLUE = (50, 153, 213)

# Clock
clock = pygame.time.Clock()

# Snake settings
BLOCK_SIZE = 10
START_SPEED = 10

# Fonts (safe)
score_font = pygame.font.SysFont("arial", 30)
message_font = pygame.font.SysFont("arial", 40)


def draw_score(score_value, level_value):
    text_surface = score_font.render(
        f"Score: {score_value}   Level: {level_value}",
        True,
        COLOR_BLACK
    )
    screen.blit(text_surface, (10, 10))


def draw_snake(block_size, snake_body):
    for block in snake_body:
        pygame.draw.rect(
            screen,
            COLOR_GREEN,
            [block[0], block[1], block_size, block_size]
        )


def show_message(text, color):
    message_surface = message_font.render(text, True, color)
    screen.blit(
        message_surface,
        (SCREEN_WIDTH / 6, SCREEN_HEIGHT / 3)
    )


def game_loop():
    game_running = True
    game_over = False

    x_position = SCREEN_WIDTH / 2
    y_position = SCREEN_HEIGHT / 2

    x_change = 0
    y_change = 0

    snake_body = []
    snake_length = 1

    food_x = round(random.randrange(0, SCREEN_WIDTH - BLOCK_SIZE) / 10) * 10
    food_y = round(random.randrange(0, SCREEN_HEIGHT - BLOCK_SIZE) / 10) * 10

    score = 0
    level = 1
    speed = START_SPEED

    while game_running:

        while game_over:
            screen.fill(COLOR_BLUE)
            show_message("Game Over! Press C to Play Again or Q to Quit", COLOR_RED)
            draw_score(score, level)
            pygame.display.update()

            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_running = False
                        game_over = False
                    if event.key == pygame.K_c:
                        game_loop()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_running = False
            elif event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x_change = -BLOCK_SIZE
                    y_change = 0
                elif event.key == pygame.K_RIGHT:
                    x_change = BLOCK_SIZE
                    y_change = 0
                elif event.key == pygame.K_UP:
                    y_change = -BLOCK_SIZE
                    x_change = 0
                elif event.key == pygame.K_DOWN:
                    y_change = BLOCK_SIZE
                    x_change = 0

        if (
            x_position >= SCREEN_WIDTH
            or x_position < 0
            or y_position >= SCREEN_HEIGHT
            or y_position < 0
        ):
            game_over = True

        x_position += x_change
        y_position += y_change

        screen.fill(COLOR_BLUE)
        pygame.draw.rect(
            screen,
            COLOR_RED,
            [food_x, food_y, BLOCK_SIZE, BLOCK_SIZE]
        )

        snake_head = [x_position, y_position]
        snake_body.append(snake_head)

        if len(snake_body) > snake_length:
            del snake_body[0]

        for block in snake_body[:-1]:
            if block == snake_head:
                game_over = True

        draw_snake(BLOCK_SIZE, snake_body)
        draw_score(score, level)

        pygame.display.update()

        if x_position == food_x and y_position == food_y:
            food_x = round(random.randrange(0, SCREEN_WIDTH - BLOCK_SIZE) / 10) * 10
            food_y = round(random.randrange(0, SCREEN_HEIGHT - BLOCK_SIZE) / 10) * 10
            snake_length += 1
            score += 10

            if score % 50 == 0:
                level += 1
                speed += 2

        clock.tick(speed)

    pygame.quit()
    quit()


game_loop()
---

## How to Run
## How to Run the Game (Windows)

### Requirements
- Python 3.10 or higher
- Pygame library

### Steps

1. Clone the repository or download the project files.

2. Open the project folder.

3. Create and activate a virtual environment (optional but recommended):

   python -m venv venv
   venv\Scripts\activate

4. Install the required dependency:

   python -m pip install pygame

5. Run the game:

   python snake_game.py

The game window will open automatically.  
Use the arrow keys to control the snake.


---

## Skills Demonstrated
- Python fundamentals
- Game loop design
- Event-driven architecture
- Coordinate-based movement systems
- Debugging and runtime error resolution

---

## Future Improvements
- Difficulty levels
- Sound effects and background music
- Persistent high-score storage
- Modular refactoring into classes

---

## Author
Aggrey Kibe  
Aspiring Software Developer & Cybersecurity Enthusiast
